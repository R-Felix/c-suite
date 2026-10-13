---
name: retrospective
description: Close a c-suite milestone with a blameless retrospective. It turns the cost ledger, returned cards, reversed decisions and the principal's corrections into rules for the project, for all of the principal's projects (house rules) or for the c-suite plugin itself, and recalibrates model routing from actual costs. Use at the end of a milestone, or when someone asks for a retro, post-mortem, lessons learned or a cost review of a project.
argument-hint: "[milestone, e.g. M2]"
---

# Retrospective

`PLAYBOOK` is `../../playbook/` from this skill's base directory. `HOUSE` is the folder named by the `C_SUITE_HOME` environment variable if it is set, otherwise `~/.claude/c-suite/`. The ops folder is
named in the project's `CLAUDE.md`, `ops/` by default. Blameless: look for causes and mechanisms, not culprits.

1. **Gather, cheaply:** the milestone's rows in `ledger.csv`; its `plan.md` (returns, abandoned cards); in
   `decisions.md`, the defaults and what the principal reversed; the principal's corrections during the milestone
   (the conversation, and feedback memories if any); incidents (`git log` of the ops folder).
2. **Numbers:** fill the retro's table, and per role: cards, median actual against estimate, returns. A short script
   is fine for the arithmetic.
3. **Analyse:** for each thing that hurt, what happened → the mechanism → the rule that would have prevented it. For
   each reversed decision, what the recommendation missed.
4. **Promote each rule to the right layer:**
   - **Project:** apply it directly to `agent-frame.md`, `CLAUDE.md` or `definition-of-done.md`, keeping them short.
   - **House** (worth it for every project of this principal): propose it; it needs the principal's yes (at night,
     put it in "For the principal"). On yes, add it to `HOUSE/house-rules.md` (at most 40 rules; merge duplicates).
   - **Suite** (worth it for everyone using c-suite): write the proposed change as text ready to file as an issue or
     pull request on the c-suite repository. Nothing is published without the principal.
5. **Calibrate:** update the table in `HOUSE/calibration.md` (role × size: tasks, median, p90, returns), merged with
   the rows already there. Write an adjustment only when a pattern holds on at least three tasks, and name the
   project and milestone it comes from.
6. **Write** `<ops>/retros/M<n>.md` from `PLAYBOOK/templates/project/retro.md` (one page, in the principal's
   language) and commit it.
7. **Report** in at most ten lines, with the house promotions to approve as numbered decisions.
