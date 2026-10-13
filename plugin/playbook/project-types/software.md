# Project type: software

Applications, tools, automations, data pipelines, websites.

## Definition of done (copied into `ops/definition-of-done.md`, then adapted)

A change is done when:
1. Its acceptance criteria are met, with evidence (commands and their results).
2. Each business rule it adds or changes has a test; each fix has a test that fails without it.
3. The quick checks pass on every commit (format, types, lint, the tests of touched files).
4. What users see works in light and dark themes, on a phone, with a keyboard, if the project has a UI.
5. It is merged by the orchestrator, never by an agent.

A release is done when the **full verification** passes once (the whole test suite and any slow checks: end-to-end,
benchmarks, mutation), it is deployed to a test environment and looked at, and the principal said yes for production.
The full verification runs **once per release**, never again for the same commit.

## Typical milestones

Scaffold (structure, build, test, run commands) → first usable slice end to end → features by user value → hardening
(errors, speed, security) → release. The scaffold card runs alone; nothing runs in parallel with it.

## Cards and roles

| Card | Role |
|---|---|
| Map the existing code, list the places to change | scout |
| A feature or fix with a clear card | builder |
| Data migration, payments, outbound email or messages, auth and permissions, a core algorithm | specialist + cold review |
| Unclear bug (root cause unknown), architecture choice, splitting a milestone | architect |
| A problem that defeated the architect | expert |

## Proof

Commands and their output (tests, build, a request and its response), screenshots for UI (light, dark, phone). An
agent's "it works" is not proof.

## Project-specific one-way doors

Deploying to production; a database migration on real data; sending real emails or messages; anything that bills;
deleting data; changing permissions or authentication; adding a paid dependency or service.

## Modules (declare them in `agent-frame.md` when they apply)

- **One worktree or branch per agent.** Agents commit on their own branch, never merge, never push; the orchestrator
  integrates. Copy into each worktree the local, untracked files the build needs (environment files, local configs).
- **Shared resource lock.** When agents share a machine with timing-sensitive checks (benchmarks, end-to-end tests),
  heavy runs take a lock (a directory created with `mkdir`, with the owner's name inside, removed right after;
  considered abandoned after a set time). While someone else holds it: code and targeted tests only.
- **Environments.** Test and production are separate; agents work against test only; the principal publishes.
- **Never `git stash` in worktrees:** the stash is shared by all worktrees of a repository. Use a temporary commit.

## Cold review checklist (in order of importance)

1. Data lost, overwritten or leaked; a message sent when it should not be (twice, to the wrong person, from a test
   environment to a real address).
2. A business rule contrary to the charter or to a decision; a state changed wrongly.
3. Races, transactions, permissions, migrations' compatibility with other branches in flight.
4. User-facing: does the whole control do the action, light and dark, phone, keyboard, accessibility.
5. Tests that prove what they claim; rules written once; no dead code.
