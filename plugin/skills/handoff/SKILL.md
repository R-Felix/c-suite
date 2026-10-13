---
name: handoff
description: Pause or resume a c-suite project cleanly. Pause writes the orchestrator's state to status.md so a fresh session can continue; resume reads it, checks it against reality, applies the principal's answers and continues with fresh agents rather than relaunching large contexts. Use when someone says pause, stop for today, we will continue later, resume, pick up where we left off, or when the orchestrator's own conversation has grown long.
argument-hint: "pause | resume"
---

# Handoff

The ops folder is named in the project's `CLAUDE.md` (`Operating files:`), `ops/` by default. With no argument:
`resume` if this session has not done any work on the project yet, otherwise `pause`.

## Pause

1. Read the clock. Let a running agent finish if it is close to done (about ten minutes); otherwise note where its
   work stands.
2. Rewrite `status.md` from its template, at most 60 lines: **Now**, **In flight** (each card: state, where its
   partial work is, what to do with it), **Waiting on the principal**, **Next**, and **Resume**: the exact steps for a
   fresh session ("check the branch of T05; relaunch T05 as a fresh builder with its card and 'continue from commit
   abc123'").
3. Commit unfinished work on its own branch (a temporary commit, never a stash), and commit the ops files. Never push
   unless the project's rules say so.
4. Tell the principal in at most five lines: where things stand, and how to resume: in a new conversation in this
   folder, "resume" (or `/c-suite:handoff resume`).

## Resume

1. Read the clock (day or night mode). Read `PLAYBOOK/operating-model.md` once (`PLAYBOOK` is `../../playbook/` from
   this skill's base directory), then `status.md`, the "For the principal" section of `decisions.md` and the current
   `plan.md`.
2. Check reality against `status.md`: git status and branches, files, locks, processes. Say what differs.
3. Apply the principal's answers given since the pause: update `decisions.md`, unblock cards, and add a card to redo
   anything built on a default they reversed.
4. **Never relaunch an old agent with a large context:** each of its turns re-reads everything. Start fresh agents on
   the cards, with the state they need.
5. Tell the principal where things stand, what happens next and when it should end. Continue with `run-milestone`.
