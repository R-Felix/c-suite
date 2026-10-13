---
name: run-milestone
description: Run a planned milestone of a c-suite project as its orchestrator (COO). Launch the right role agent for each ready task card (at most two at a time), accept work on evidence, return or escalate it, record each task's cost in the ledger, keep status and decisions current, and follow the day and night rules for questions. Use when someone asks to run, execute, continue or carry out a milestone of a project that has an ops folder.
argument-hint: "[milestone, e.g. M2]"
---

# Run a milestone

`PLAYBOOK` is `../../playbook/` from this skill's base directory. The ops folder is named in the project's
`CLAUDE.md` (`Operating files:`), `ops/` by default. The operating model (`PLAYBOOK/operating-model.md`) applies
throughout: read it once per session if you have not.

## 0. Prepare

1. Read the clock: day or night mode (principal profile).
2. Read `status.md`, the milestone's `plan.md`, and the "For the principal" section of `decisions.md`. Skim
   `agent-frame.md` (agents read it in full; you need to know what it says).
3. **Check status against reality** (git status and branches, files, locks, agents still running). Fix `status.md`
   first if they differ.
4. **Progress display.** If `mcp__savvy-progress__progress` exists (load it with ToolSearch if deferred), call it with
   `title` "M<n> · <title>", `total`, `tasks` (`{title, tier, after}` per card, in plan order) and `phase: "delegate"`.
   Tiers by role: scout → `light`, builder → `medium`, specialist → `careful`, architect → `heavy`, reviewer →
   `medium`, expert → `fable`. Otherwise, the status column of `plan.md` is the display.
5. Tell the principal in two lines: how many cards, the estimate, the end time.

## 1. The loop

Repeat until no card is ready:

**a. Pick.** Ready cards are those whose dependencies are accepted and that are not blocked. At most two at a time,
never two that write the same files or hold the same shared resource.

**b. Launch.** Agent tool:
- `subagent_type`: `c-suite:<role>` (if the list shows it without the prefix, the bare `<role>`; if it shows neither,
  `general-purpose` with the model of `PLAYBOOK/routing.md`, and note it in `status.md`);
- `description`: the card's title, verbatim;
- `prompt`: "Read `<ops>/agent-frame.md`, then your card `<ops>/milestones/<M>/<card>.md`, and do it." plus at most
  five lines of live context (where a previous card left its output, a decision just taken). Never paste the frame or
  the card;
- `model`: only if the card says so.

Run in the background whenever something else can proceed. Mark the card `running`.

**c. While agents work,** do not duplicate their work. Prepare the next launches, answer the principal, keep
`status.md` current.

**d. Accept on evidence.** For each criterion of the card, is the evidence there and credible? Re-run the cheap checks
yourself (a command, open the file, look at the screenshot). For a high-risk card, read the actual output or diff.
- `Review: cold` → launch a `reviewer` with the card, what to review (paths, commit) and the cold review checklist of
  the project type; its findings feed your decision.
- Then **accept**, **return** (a *fresh* agent of the same role with the card and a precise defect list; on the second
  return, one role up), or **take over** (trivial fixes only). After two returns, re-plan the card (architect) or ask
  the principal.

**e. Record**, whatever the outcome:
- one row in `ledger.csv`: date, milestone, card, role, model, effort, size, estimate, actual (the k tokens the Agent
  result reports, empty if it reports none), tool uses, minutes, outcome (`accepted`, `returned`, `abandoned`), round,
  a short note;
- the card's status in `plan.md`; the progress display (`done` = cards accepted);
- the choices in the report: two-way doors decided by your recommendation and logged as `default (day)` or
  `default (night)`; one-way doors added to "For the principal", and the cards they block marked;
- the lines of `status.md` that changed;
- for software, integration as the project's modules say (the orchestrator merges; quick checks per change; the full
  verification once per release).

**f. Read the clock.** Entering night mode: post a short end-of-day summary, then stop asking and notifying. Entering
day mode: the first message to the principal is the "For the principal" section.

**g. Talk to the principal** when something happens (a result to look at, a decision needed, a problem), not at each
event. In day mode, group questions in one numbered message. Send a phone notification (if the tool exists and the
profile allows it) only when every remaining card is blocked on them, or for an action only they can do (a login, an
approval). Never at night, never for progress.

## 2. Stop and tell the principal when

- every remaining card is blocked on one-way doors;
- the actual cost passes 1.5 times the milestone's estimate, or a cost falls outside the charter's budget;
- a card failed twice;
- something contradicts the charter;
- your own conversation is getting long (roughly ten cards, or a lot of reading): run `handoff pause` and continue in
  a fresh session.

## 3. Close the milestone

1. Every card is accepted, or abandoned with its reason; the milestone's "done when" is checked with evidence.
2. Roadmap: `done` and dates. `status.md` updated. Progress: `finished: true`.
3. Report in at most 15 lines: what was delivered and where to look; what was verified; the cost (estimate and
   actual); the decisions table; what comes next. End with the closing block (operating model §6).
4. Commit the ops files. Run `retrospective`, or offer it if the principal wants to look at the result first.
