# Changelog

## 0.2.0 — 2026-10-14

Economy rules learned from the first pilot (one night of three agents cost about 1.5 M tokens):

- Workers run only the checks for what they touched; the orchestrator runs the full verification once, at
  integration.
- Two failures of the same kind stop the loop: the agent reports instead of retrying.
- A card is time-boxed: past twice its estimated duration, the agent stops and reports.
- Screenshots only when the principal must see something or the card is visual.
- One agent at a time in night mode.

## 0.1.0 — 2026-10-13

First version: the operating model, routing table, templates, three project types (software, research, content),
six skills (start-project, plan-milestone, run-milestone, handoff, retrospective, decision-brief) and six agent roles
(scout, builder, specialist, architect, reviewer, expert).
