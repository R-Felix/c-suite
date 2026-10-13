# c-suite

**Run any project like a well-managed company.** You are the principal (the CEO): you own the *what*. Claude is the
orchestrator (the COO): it owns the *how*, and runs a team of role-based agents, each with the right model and effort
for its task.

c-suite is a [Claude Code](https://claude.com/claude-code) plugin. It packages an operating model that grew out of
weeks of real work on a production CRM (software), and generalises it to research and content projects. It is built
to be **frugal with tokens**, **reliable** (work is accepted on evidence, not on an agent's word) and **learning**
(every correction becomes a rule at the right level).

> Langue maternelle : the plugin is written in English, but it works in yours. Your profile sets the language of
> every message and document; see [README.fr.md](README.fr.md) for French.

## What you get

| Skill | When | What it does |
|---|---|---|
| `/c-suite:start-project` | Day one | A short interview, then the charter (outcome, success measures, budget, out of scope, **pre-mortem**), the definition of done, the roadmap, the decision log, the cost ledger and the agent frame |
| `/c-suite:plan-milestone` | Before each milestone | Task cards: objective, exact inputs, outputs, verifiable acceptance criteria, scope, size, role (model and effort), review level, dependencies; with a cost estimate and an end time |
| `/c-suite:run-milestone` | During | The COO loop: at most two agents at a time, acceptance on evidence, returns and escalation, cost ledger, decision log, **day and night rules** |
| `/c-suite:handoff` | Pause or resume | A state file a fresh session can resume from, so nobody relaunches a huge context |
| `/c-suite:retrospective` | After each milestone | Blameless review; rules promoted to the project, to all your projects, or to c-suite itself; routing recalibrated from actual costs |
| `/c-suite:decision-brief` | Any hard call | One page: options compared on effects, cost, reversibility and risk; a recommendation; the cheap test that settles the doubt |

Six agent roles, each with its model and effort set in its definition, so routing is structural:

| Role | Model · effort | For |
|---|---|---|
| `scout` | Haiku · low | Reading, inventories, extraction, summaries (read-only) |
| `builder` | Sonnet · medium | Clear cards with ordinary risk: most of the work |
| `specialist` | Opus · high | Clear cards with high stakes: data, money, outbound messages, security |
| `architect` | Opus · xhigh | Unclear problems: investigate, design, split into cards |
| `reviewer` | Sonnet · high | Cold, read-only reviews of high-risk results |
| `expert` | Fable · high | Reserve: what defeated the architect, or on request |

## Principles

- **The *what* is yours, the *how* is Claude's.** Before anything reaches real users, most choices are reversible:
  Claude decides them by default and logs them so you can reverse them.
- **One-way and two-way doors.** Irreversible things, money outside the budget, publishing or sending to real people,
  personal data and changes to the charter wait for you. Everything else moves.
- **Day and night.** Claude reads the clock. During your working hours it asks, grouped and numbered. Outside them it
  never waits and never notifies: it decides what is reversible, parks the rest, and greets you in the morning with a
  numbered list of decisions to confirm or reverse.
- **Task cards are contracts.** Workers cannot see your conversation; the card and the project's agent frame are
  their whole world.
- **Acceptance is by evidence.** A report is a claim; Claude checks it. Cold reviews only where the risk justifies them.
- **Frugal by design.** Shared context written once and referenced, exact inputs, one-hour cards, the cheapest role
  that succeeds the first time, one or two agents at a time, fresh agents rather than relaunches, short reports, full
  verification once per release.
- **A cost ledger.** Every task records its estimated and actual cost; retrospectives recalibrate the routing.
- **An organisation that learns.** Three layers of rules: c-suite (universal), house (yours, for all your projects),
  project. Retrospectives promote what they learn upward.

Inspired by Amazon (working backwards; one-way and two-way doors), Intel (task-relevant maturity), Apple (a directly
responsible owner per task), Netflix (context, not control), Google (blameless post-mortems) and the pre-mortem.

## Install

```bash
claude plugin marketplace add OWNER/c-suite
claude plugin install c-suite@c-suite
```

Then, in an empty folder (or an existing project): `/c-suite:start-project`. The first time, it asks a few questions
about you (name, language, working hours, notifications, budget) and writes your profile to `~/.claude/c-suite/`.

Each project's `CLAUDE.md` imports your profile and house rules from there; Claude Code asks once per project to
allow these imports: accept. Set `C_SUITE_HOME` to use another folder (tests, several profiles).

Optional: the [savvy-progress](https://github.com/johnnyvizz/claude-kit) mod shows a progress bar of the milestone;
c-suite uses it when it is installed.

## What a project looks like

```
CLAUDE.md                  short: the principal, the outcome, where things are
ops/
  charter.md               the principal's document
  definition-of-done.md
  roadmap.md
  status.md                the orchestrator's state, for any fresh session
  decisions.md             numbered; what awaits the principal on top
  ledger.csv               one row per task: role, model, estimate, actual, outcome
  agent-frame.md           what every agent reads first
  milestones/M1-…/         plan.md and one card per task
  retros/
```

## Project types

`software`, `research` (studies, analyses, due diligence) and `content` (campaigns, sequences, documentation). Each
brings its definition of done, typical milestones, card archetypes, proof standards, one-way doors and cold review
checklist. Other kinds of projects start from the closest type.

## Contributing

Retrospectives produce "suite" rules: improvements worth sharing with everyone. Open an issue or a pull request with
the rule, its reason and the evidence from your ledger.

## License

MIT
