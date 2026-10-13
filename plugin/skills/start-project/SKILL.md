---
name: start-project
description: Start a new project the c-suite way, with the user as principal (CEO) and Claude as orchestrator (COO) of role-based agents. A short interview, then the charter, pre-mortem, definition of done, roadmap, decision log, cost ledger and agent frame. Use when someone wants to start, launch or kick off a project of any kind (software, research, content, campaign), in any language ("démarrer un projet", "lancer un nouveau projet").
argument-hint: "[project name or one-line idea]"
---

# Start a project

`PLAYBOOK` is `../../playbook/` from this skill's base directory. `HOUSE` is the folder named by the `C_SUITE_HOME` environment variable if it is set, otherwise `~/.claude/c-suite/`.

The principal is present when this skill runs: it is their project, so the charter is theirs to approve. Everything
you write for them is in their language (principal profile); file names stay in English.

## 0. Prepare

1. Read `PLAYBOOK/operating-model.md` once for this session. Read the clock (`date`, or `Get-Date` in PowerShell).
2. If `HOUSE/principal.md` does not exist, run the **principal interview** (§1) first. Otherwise read it.
3. Look at the working directory:
   - **Already run with c-suite** (a `CLAUDE.md` line `Operating files:`, or `ops/charter.md`): stop. Say so and offer
     `plan-milestone`, `run-milestone` or `handoff resume`.
   - **Existing content** (code, documents): adopt it. Launch one `scout` to inventory it in at most one page (what it
     is, its state, its commands, its documents). The charter describes the project from now on.
   - **Empty:** a new project.
   - The ops folder is `ops/`, unless `ops/` already serves another purpose: then `c-suite/`.

## 1. Principal interview (first time only)

One message, every question with a proposed answer taken from what you can see (the conversation's language, the
clock's time zone, memories, an existing `CLAUDE.md`), so the principal can answer "ok" or correct a few lines:

1. Name, and how to address them.
2. Language for messages and documents; language of agents' reports ("same", or English to save tokens).
3. Time zone and working hours (night mode outside them: no questions, no notifications, decisions by default).
4. Phone notifications: when, if ever.
5. Budget sensitivity (plan, limits already hit, money available for tools and services).
6. Areas never to touch without asking, beyond the operating model's one-way doors.

Write `HOUSE/principal.md` from `PLAYBOOK/templates/house/principal.md`. Copy `house-rules.md` and `calibration.md`
from the same folder if they are missing. Tell the principal these files are theirs to edit and apply to all their
projects.

## 2. Project interview

One message, at most eight questions, each with a proposed answer; skip what the request already answers:

1. **The outcome, from the finish line:** the day it is done, what has changed, for whom?
2. **For whom** exactly (users, readers, clients, the team)?
3. **Success measures:** how will we know, with what target?
4. **Deadline and budget:** money, usage limits, the principal's own time.
5. **Constraints:** what must or must not be used; who else is involved.
6. **Out of scope.**
7. **Project type:** software, research and analysis, or content and campaigns (`PLAYBOOK/project-types/`). For
   anything else, take the closest type and say what you adapt.
8. **What worries you most?** (It seeds the pre-mortem.)

## 3. Set up

Write, in the principal's language, from `PLAYBOOK/templates/project/` (translate the headings, remove the comments
once filled):

| File | Content |
|---|---|
| `CLAUDE.md` | From the template, under 40 lines. If a `CLAUDE.md` exists, insert the c-suite block at its top; never drop its content. |
| `<ops>/charter.md` | From the interview. You draft the pre-mortem: 5 to 8 causes, the principal's worry among them, each with its early signal and mitigation. |
| `<ops>/definition-of-done.md` | The project type's definition of done, adapted to the charter. |
| `<ops>/roadmap.md` | 3 to 7 milestones from the type's typical milestones; each delivers something the principal can judge. |
| `<ops>/decisions.md` | The kickoff decisions (project type, milestone order, every assumption you made), numbered, with a recommendation and a concrete stake. |
| `<ops>/agent-frame.md` | The project in five lines; prohibitions from the type's one-way doors and the principal's "never"; the type's modules that apply. |
| `<ops>/status.md`, `<ops>/ledger.csv` | From the templates. |

Then, if the directory is not a git repository, `git init` and commit the files ("Start the project with c-suite").
Never push.

## 4. Present and hand over

In at most 20 lines: the outcome in two lines, the success measures, the roadmap table, the three main pre-mortem
risks, and the decisions table, ending with the closing block (operating model §6). **Ask the principal to approve the charter**: it is their document (a one-way door).
Log the approval in `decisions.md`.

Next step: `plan-milestone` for M1. If the principal already said to go ahead, continue with it directly.
