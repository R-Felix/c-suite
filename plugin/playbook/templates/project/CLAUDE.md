# {{project_name}}

<!-- Loaded into every session and every agent of this project: keep it under 40 lines. Only what an agent cannot
derive and would otherwise get wrong. Written in the principal's language. -->

@~/.claude/c-suite/principal.md
@~/.claude/c-suite/house-rules.md

<!-- The two imports above load the principal's profile and house rules (Claude Code asks once per project to allow
imports from outside the project: accept). The next line keeps the essentials if they are not loaded. -->
- **Principal:** {{name}} · always write in {{language}} · profile: `~/.claude/c-suite/principal.md`.
- **Run with c-suite.** Operating files: `{{ops}}/` (charter, roadmap, status, decisions, ledger, agent frame,
  milestones). Operating model: the c-suite plugin.
- **Outcome:** {{one_line_outcome}} (details: `{{ops}}/charter.md`).
- **Project type:** {{project_type}}. Done means `{{ops}}/definition-of-done.md`.
- **Resume a session:** read `{{ops}}/status.md` first.

## Project rules

<!-- Commands (build, test, run), conventions, places, tools: only the non-obvious ones. -->
