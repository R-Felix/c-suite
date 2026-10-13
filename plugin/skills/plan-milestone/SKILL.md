---
name: plan-milestone
description: Split a milestone of a c-suite project into task cards, the specification each agent works from (objective, exact inputs, outputs, verifiable acceptance criteria, scope, size, role with its model and effort, review level, dependencies), and estimate its cost and end time. Use after start-project, or when someone asks to plan, break down or prepare the next milestone or phase of a project that has an ops folder.
argument-hint: "[milestone, e.g. M2]"
---

# Plan a milestone

`PLAYBOOK` is `../../playbook/` from this skill's base directory. `HOUSE` is the folder named by the `C_SUITE_HOME` environment variable if it is set, otherwise `~/.claude/c-suite/`. The ops folder is
named in the project's `CLAUDE.md` (`Operating files:`), `ops/` by default.

## 0. Prepare

1. Read once per session: `PLAYBOOK/operating-model.md`, `PLAYBOOK/routing.md`, the "Cards and roles" and "Proof"
   sections of the project type (`PLAYBOOK/project-types/`), and `HOUSE/calibration.md`. Read the clock.
2. From the ops folder, read: the charter (outcome, constraints, pre-mortem), the milestone's row in the roadmap, the
   definition of done, the open and relevant decisions, and `status.md`.
3. The milestone is the argument, or the first one not done. Mark it `planning` in the roadmap.

## 1. Understand before cutting

- If cutting would require reading a lot, run one `scout` card first (an inventory or summary of at most one page).
- If the problem itself is unclear, run one `architect` card: it investigates and writes draft cards in the milestone
  folder; you review and finalize them. You keep the final say on the plan.
- Otherwise, write the cards yourself.

## 2. Cut into cards

Write `<ops>/milestones/M<n>-<slug>/plan.md` and one `T<nn>-<slug>.md` per card, from the templates in
`PLAYBOOK/templates/project/` (`milestone-plan.md`, `task-card.md`), in the agents' language. The rules:

- **One owner, one outcome**, judged by acceptance criteria that can be checked: a command and its expected result, an
  observation, an exact success phrase. Use the project type's "Proof".
- **Size S or M** (calibration medians if known; otherwise S ≈ 40k and M ≈ 100k tokens to estimate). Larger: split.
- **Inputs are exact:** paths and sections, decisions by number, and only the context the files do not give. A card
  must make sense without this conversation.
- **Role** by the two questions of `routing.md`, adjusted by the calibration. **Review: cold** only for high risk.
- **Dependencies** form a chain or a tree; at most two cards run at once; two cards that write the same files or use
  the same shared resource never run at the same time.
- **Titles** of at most six words, unique: they become the Agent descriptions and the progress bar's labels.
- A greenfield software project starts with a scaffold card that runs alone.
- A card that would cross a one-way door is marked `blocked (D<n>)`, and `D<n>` goes to `decisions.md`.

Before presenting, check: every card answers "how will we know it is done?"; none needs the conversation to be
understood; no two parallel cards collide.

## 3. Estimate

Sum the cards' estimates (k tokens), the agent hours, and the wall-clock time with at most two agents in parallel.
Give the end time as a clock time.

## 4. Present

At most 15 lines: the plan table, the estimate and end time, and the decisions for the principal (numbered,
recommendation, concrete stake), as the closing block (operating model §6). In day mode, ask before running if the plan crosses a one-way door or departs from
the roadmap; otherwise proceed. In night mode, proceed with what is not blocked.

Unless the principal asked to stop at the plan, continue with `run-milestone`.
