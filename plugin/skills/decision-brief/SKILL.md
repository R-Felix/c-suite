---
name: decision-brief
description: Prepare a hard decision on one page. The question, what is at stake, two to four options compared on effects, cost, reversibility and risk, a recommendation and what would change it, verified versus inferred facts, and the cheap test that would settle the doubt. Use when someone faces a difficult choice, asks to weigh options, compare alternatives, arbitrate or decide ("aide-moi à trancher", "arbitrer"), inside or outside a c-suite project.
argument-hint: "[the question]"
---

# Decision brief

`PLAYBOOK` is `../../playbook/` from this skill's base directory. Write in the principal's language (`principal.md` in the
folder named by `C_SUITE_HOME`, otherwise in `~/.claude/c-suite/`; else the conversation's language).

1. **Frame.** The question in one line, the deadline and why then, and whether it is a one-way or a two-way door
   (`PLAYBOOK/operating-model.md` §3). If the question is fuzzy, restate it and confirm it (or, at night, state your
   framing and go on).
2. **Gather only the facts the comparison needs**, cheaply: a `scout` for reading and inventories, a web search for
   outside facts, an `architect` only if the problem itself needs investigating. Label each fact **verified** (where)
   or **inferred** (why).
3. **Options:** two to four, including "do nothing" or "later" when that is a real option. For each: what changes for
   people, the cost (money, time, usage), whether it can be undone, the main risk, and what the principal must do.
4. **Recommend** one option, with a confidence (high, medium, low) and the fact that would change it. If confidence
   is not high, design the cheap test: the smallest experiment that would settle it, its cost and duration.
5. **Write** from `PLAYBOOK/templates/project/decision-brief.md`. In a c-suite project:
   `<ops>/decisions/D<n>-<slug>.md`, plus a row in the "For the principal" section of `decisions.md`. Otherwise, in
   the conversation, or in a file if asked.
6. **Present** in at most 12 lines: the question, the recommendation, the condensed comparison and the stake. The
   principal decides; log the decision. End with the closing block (operating model §6).
