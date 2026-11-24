# AGENTS.md

Guidance for coding agents working in this repository. `CLAUDE.md` imports this file and adds nothing.

## What this repository is

A collection of agent skills that restyle AI-generated interfaces of any kind: dashboards, tables, forms, landing pages, mobile screens, flows. It is documentation: no build, no lint, no tests. It is distributed through `npx skills add bogdanptr/unslop` and as the Claude Code plugin `unslop`, defined in `.claude-plugin/`.

Bump `version` in `.claude-plugin/plugin.json` in the same commit as any change under `skills/` or `agents/`. Plugin users only receive updates when that number changes.

## Structure

```
skills/<name>/SKILL.md        entry point, frontmatter with name and description
skills/<name>/<topic>.md      reference files, linked from the principle that needs them
skills/<name>/agents/openai.yaml   Codex display metadata
agents/<name>.md              Claude Code subagents: auditor, screen worker, critic
```

Four kinds of skill:

- **The orchestrator**, `unslop`. It owns the pipeline, the content contract, the subagent briefs and the report format. It holds no design rules.
- **The fundamentals**, `unslop-principles`. It holds the design laws every pass is judged by, each with a test, and no values.
- **Pass skills**: `unslop-diagnose`, `unslop-direction`, `unslop-layout`, `unslop-surfaces`, `unslop-dataviz`, `unslop-typography`, `unslop-color`, `unslop-navigation`, `unslop-verify`. Each owns one domain's rules.
- **Adapters**: `unslop-figma` and `unslop-code`. They own mechanics for a source type and no design rules.

## Rule ownership

Each rule lives in one skill. Other skills point to it by skill name in backticks, never by a relative link across skill folders, because a skill may be installed alone.

| Topic | Owner |
| --- | --- |
| What may be cut, the ledger, modes, pass order | `unslop` |
| The fundamentals and their tests, what premium means in decisions | `unslop-principles` |
| The catalog of tells | `unslop-diagnose` |
| The kinds of screen, the brief and its five dials | `unslop-direction` |
| The focal point per kind of screen, cutting decisions, grids, spacing scale, widths, alignment | `unslop-layout` |
| Containers, borders, radius, icons, shadows, buttons, inputs, rows, overlays, materials | `unslop-surfaces` |
| Chart forms, a main figure's form, number and unit styling, deltas, tables | `unslop-dataviz` |
| Typeface, weights, sizes, tones, overlines | `unslop-typography` |
| Background, palette roles, accent, status colors, contrast | `unslop-color` |
| Tab bars, sidebars, top navigation, headers, interface labels | `unslop-navigation` |
| Parity, re-scan, verdict | `unslop-verify` |

When a rule could sit in two skills, put it with the owner of the underlying decision and leave a one-line hand-off in the other.

## Authoring conventions

Every `SKILL.md` has:

- **Frontmatter** with `name`, matching the folder, and a `description` that says what the skill does and when to use it, including the words a user would type.
- **A plain H1 and a short opener** saying what the skill is and does.
- **A hand-off paragraph** naming the sibling skills that own adjacent topics.
- **A calibration section** with a heading that carries its point. It says which parts are judgment and which are exact, and what the skill does in `reskin` mode.
- **Headings that state the rule**, in sentence case. Number them only when the steps run in order, or when other skills cite them by number.
- **Exact values.** A range with a default, not "subtle" or "generous".
- **A `## Before you finish` table**: what you notice on the left, the fix on the right. The left column is a detection pattern an agent can search for.

Writing rules:

- Write for an agent with no context. Say what to do and give the value.
- Explain why once, briefly, where the reason changes how the rule is applied.
- **Every rule is general.** It must hold for a phone summary screen, a desktop dashboard, a settings form and a landing page, or say which kinds of screen it applies to, using the kinds defined in `unslop-direction`. A rule that only makes sense for one product does not belong in a skill.
- **Examples vary and belong to no one.** Draw them from different products and kinds of screen, so no skill reads as a recipe for one app. Do not name or describe a specific design this collection was built or tested on. An example is a generic product type with invented values, and no single case supplies more than one or two examples in a skill.
- A principle with no test and a rule with no value are both unfinished. Fundamentals go in `unslop-principles` with a test. Values go in the pass skill that owns them.
- Any color value published here is computed, not estimated. Contrast ratios in `unslop-color` and `unslop-surfaces` were calculated from the listed values. Recompute them when a value changes.
- Reference files carry recipes and tables. They do not restate the principle, and the principle does not summarize the recipe.

## The content contract is the product

The promise of this collection is that a restyle keeps the content. Any change that weakens that, such as letting a pass invent sample data or reword a value, is a regression however good the output looks. When editing a pass skill, check that its `reskin` behaviour and its hand-off to the contract are still stated.
