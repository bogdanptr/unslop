---
name: unslop
description: Takes any AI-generated interface - dashboard, table, form, landing page, mobile screen, flow - from Figma, code or a screenshot and restyles it into a distinctive, premium version while keeping its content and data. Runs the unslop-* skills in order - diagnose, direction, layout, surfaces, dataviz, typography, color, navigation, verify. Use when a design looks AI-made, generic or templated, or when asked to unslop, reskin, restyle, redesign, polish or make a UI look premium or design-led.
---

# Unslop

This skill runs the whole pipeline. It takes one or more screens, records what they contain, finds what makes them look machine-made, commits to one visual direction, then runs the passes in a fixed order and checks the result against the original.

Orchestration is all it owns. The fundamentals every pass is judged by belong to `unslop-principles`. The catalog of tells belongs to `unslop-diagnose`, the idea to `unslop-direction`, structure to `unslop-layout`, containers, controls, icons and material to `unslop-surfaces`, figures, charts and tables to `unslop-dataviz`, type to `unslop-typography`, background and palette to `unslop-color`, navigation and labels to `unslop-navigation`, and the final check to `unslop-verify`. Reading and writing Figma is `unslop-figma`. Restyling code is `unslop-code`.

## The look changes, the content does not

A reskin that invents a metric or drops a setting is a different product, not a better design. Before anything is restyled, every element on the screen goes into a content contract, and every element in the contract is accounted for at the end.

- Data values, names, units and user copy are carried over character for character.
- Every action keeps its destination. Every state the source has still exists.
- Nothing is invented. A new figure that needs a value the source does not have is built with a marked placeholder and reported.
- Nothing disappears silently. Whatever is cut, merged or moved is listed in the ledger with where it went.

The format and the rules for cutting are in [content-contract.md](content-contract.md).

## Three modes

| Mode | What may change | Use when |
| --- | --- | --- |
| `full` | Look, structure, chart forms, navigation items and labels. Elements may be cut or demoted, each one listed. | The default. "Unslop this", "make it premium". |
| `reskin` | Look only. Same elements, same order of sections, same labels, same navigation. | "Keep everything, just restyle", production screens with fixed scope. |
| `audit` | Nothing. Runs steps 1 to 3 and reports. | "Why does this look AI-made?" |

State the mode in the first line of the report. When the request does not say, use `full` whenever the result is written to a copy: a Figma copy, a new branch or a separate output file. Use `reskin` when editing production code in place.

## 1. Take the screen in

| Source | Adapter | You hold at the end |
| --- | --- | --- |
| Figma link or selection | `unslop-figma` | A screenshot of every frame, its layer tree and its values |
| Code in the workspace | `unslop-code` | The files that render the screen, the stack and tokens, and a screenshot if a browser is available |
| Screenshot or image only | `unslop-code`, **From a screenshot** | Every string transcribed, sizes estimated at a stated scale |

Find the product's own rules before judging anything: brand colors, a brand typeface, a design-system doc, tokens, `AGENTS.md`, `CLAUDE.md`. A documented brand decision is fixed. The direction works inside it.

## 2. Write the content contract

List every element with its exact value, following [content-contract.md](content-contract.md). This step is done when someone could rebuild the screen's information from the table alone, without the screenshot.

## 3. Diagnose

Run `unslop-diagnose` on the source. It returns the tells found, ranked by how much of the generic look each one carries, with the skill that owns each fix. In `audit` mode, report and stop here.

## 4. Commit to one direction

Run `unslop-direction`. It returns a brief of a few lines: what the product is about, the view's one job, the kind of screen it is, and the five dials (atmosphere, signature, type voice, material, accent source). The kind of screen sets how loud the restyle may be: a dashboard, a form and a landing page do not get the same treatment. Every later pass reads its decisions from the brief. A pass that needs a decision the brief does not make goes back to the brief, never to a default.

Do not stop for approval. The work happens on a Figma copy or a branch, so the user judges the result, not a description of it.

## 5. Run the passes in this order

Structure comes before skin. A palette applied to the wrong layout is repainted when the layout moves, and a material on a card that should not exist is wasted.

| # | Pass | Skill | The question it answers | Skipped in `reskin` |
| --- | --- | --- | --- | --- |
| 1 | Layout | `unslop-layout` | What is the one thing this view is about, and what can go? | Cuts and reordering |
| 2 | Surfaces | `unslop-surfaces` | Which boxes, borders and icon tiles have not earned their place? | No |
| 3 | Figures | `unslop-dataviz` | Is each figure, chart and table in the form that fits what the reader compares? | Changing a chart's form |
| 4 | Type | `unslop-typography` | Does the typeface have a voice, and is the scale right for this kind of screen? | No |
| 5 | Color | `unslop-color` | Is the background a decision, and does every color come from it? | No |
| 6 | Navigation | `unslop-navigation` | Fewer destinations, clearer names? | Yes, restyle only |
| 7 | Finish | `unslop-surfaces`, **The material goes on last** | Is the brief's material applied the same way everywhere? | No |
| 8 | Premium bar | `unslop-principles`, **Correct is not finished** | The result is correct. Is it also something worth looking at? | No, limited to what styling can add |

Run every pass even when its domain looked fine in the diagnosis. A pass that changes nothing says so in one line. A pass whose domain is absent, such as figures on a settings form or navigation in a dialog, is skipped with one line saying why.

Every pass is judged by `unslop-principles`. When a pass rule and a principle disagree for this screen, the principle wins and the report says so.

After each pass, look at the result before starting the next: a Figma screenshot, a browser screenshot, or a re-read of the diff when neither exists. When the whole result is one new file, passes may be written together, and then there are three renders at least: after the structure (passes 1 to 3), after the finish (pass 7) and after the premium bar (pass 8). Each render is looked at and its problems fixed before going on.

Pass 8 is not optional and is not a review. It changes the result. A restyle that is tidy and plain has not finished.

## 6. Verify with fresh eyes

Run `unslop-verify` against the source and the result. It checks content parity against the contract, re-scans for tells, measures contrast on the new background and stress-tests with long strings. Fix what it finds, then run it again. This step is done when the verdict is `Ship` or every remaining item is a question for the user.

## 7. Report

Use [report-format.md](report-format.md): the direction in one line, a Before, After, Why table, the content ledger and what was not verified. Keep it short. The result is the deliverable; the report explains it.

## Subagents

Where the harness can spawn subagents, three roles are worth a separate context. The auditor diagnoses without knowing what you plan to do. Screen workers restyle several screens in parallel once the direction is locked. The critic verifies without having watched the work. Briefs, what each role may touch and the sequential fallback are in [subagents.md](subagents.md).

Passes on one screen always run in sequence in one context. They edit the same nodes and the same files.

## When a skill is missing

If an owning skill is not installed, say so, skip that pass and list it under **Not done** in the report. Do not rebuild its rules from memory.

## Before you finish

| You notice | Fix |
| --- | --- |
| Restyling started with no content contract written | Stop and write it from the source, not from the restyled version |
| The original Figma frame or the main branch was edited | Restore it and redo the work on a copy or branch |
| A number, name or label in the result that is not in the contract | Replace it with the source value, or mark it as a placeholder and report it |
| A contract row with no place in the result and no ledger entry | Put it back or add the ledger entry with where it went |
| Color or material applied before the layout pass | Finish layout first, then redo the later pass |
| Two passes made opposite decisions, such as warm accent and cool glass | Reread the brief and bring both back to it |
| The result changed the palette and nothing else | That is a recolor. Run the layout, surfaces and figures passes |
| A work view, form or table given a gradient background, glass or a large hero | The brief ignored the kind of screen. Go back to `unslop-direction` |
| Every screen of a product restyled as if it were a landing page | Set the strength per kind of screen |
| "Looks premium" in the report with no screenshot looked at | Look at the render, or say it is unverified |
| The report itself calls the result plain, safe or generic | That is pass 8 not done. Go back and do it |
| Pass 8 skipped because the view is a dashboard, a form or a table | Every kind of view gets it. The brief's `Strength:` line says where |
