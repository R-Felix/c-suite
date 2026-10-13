# Routing: which role, model and effort

A card's **role** is the subagent the orchestrator launches (`c-suite:<role>`). Each role fixes a model and an effort
in its definition, so routing is a property of the card, not of the orchestrator's memory. The Agent tool's `model`
parameter may override it for one call (for example a reviewer escalated to Opus on the riskiest change); say why in
the card.

## The roles

| Role | Model · effort | Use for | Never for |
|---|---|---|---|
| `scout` | Haiku · low | Find, inventory, extract, summarize, compare files or pages; run a command and report. Read-only | Judgment calls, writing deliverables |
| `builder` | Sonnet · medium | A clear card with ordinary risk: most of the work (code, text, tables, analyses) | Unclear problems, high stakes |
| `specialist` | Opus · high | A clear card with high stakes: data migrations, money, outbound messages, security, core invariants | Exploration |
| `architect` | Opus · xhigh | An unclear problem: investigate, design, split a milestone into cards. Produces cards and decisions, not deliverables | Routine execution |
| `reviewer` | Sonnet · high | A cold, read-only review of a high-risk result, ordered by risk | Rewriting the work |
| `expert` | Fable · high | Reserve: a problem that defeated an architect, or when the principal asks | Anything else |

## The two questions

1. **Is the problem clear?** No → `architect` first (it writes the cards); a pure inventory → `scout`.
2. **What does a mistake cost?** Ordinary → `builder`. Data, money, people, security or the core → `specialist`, with
   `Review: cold`.

In doubt between two roles, take the higher one: a redo costs more than the price difference. A task that needs both
insight and care is two cards: the architect investigates and writes a precise card, the specialist executes it.

## Relative cost

Prices per million tokens (input / output), Anthropic API list prices cached on 2026-10-06; on a subscription, usage
limits play the role of money and heavier models use them faster.

| Model | Input | Output | Output cost relative to Haiku |
|---|---|---|---|
| Haiku 5.5 | $0.10 | $0.50 | 1× |
| Sonnet 5.5 | $2 | $10 | 20× |
| Opus 5.5 | $4 | $20 | 40× |
| Fable 5.1 | $10 | $50 | 100× |

What this means:

- **Haiku is twenty times cheaper than Sonnet.** Anything reading-heavy and judgment-light goes to a scout: the
  saving is large and the risk small, because the orchestrator acts on the summary, not on the scout's judgment.
- **Opus is only twice Sonnet.** When a Sonnet attempt has a real chance of being returned, Opus is cheaper per
  accepted task.
- **Effort is the second lever.** Lower effort means fewer tool calls, less preamble and terser reports. Raise it for
  risk and ambiguity, not for size.
- Fable is a reserve: two and a half times Opus.

## Calibration

These defaults are a starting point. The `ledger.csv` of each project records the role, size, estimate and actual
cost of each task, and its outcome (accepted, returned, abandoned). The retrospective compares them and writes the
principal's adjustments to `~/.claude/c-suite/calibration.md` (for example "content builders on this kind of task
are returned 40% of the time: route to specialist"), which every later plan reads.

The orchestrator's own model is the principal's choice; a strong model at medium or high effort is the reference.
