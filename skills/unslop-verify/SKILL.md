---
name: unslop-verify
description: Checks a restyled screen against its original. Confirms every piece of content and every action survived, re-scans for AI tells, measures text contrast on the new background, stress-tests with long strings and narrow widths, and returns a Ship or Fix first verdict. Read-only. Use after any restyle or reskin, as the last step of unslop, or when asked whether a redesign kept everything.
---

# Verify

This skill compares a restyled screen with its source and decides whether it is ready. It answers two questions in order: is everything still there, and does it still look generated. It reads and reports. Fixing is the job of whoever did the work.

The contract and ledger it checks against belong to `unslop`. The catalog of tells belongs to `unslop-diagnose`. Each fix goes back to the skill that owns it: `unslop-layout`, `unslop-surfaces`, `unslop-dataviz`, `unslop-typography`, `unslop-color` or `unslop-navigation`.

## Content first, looks second

A missing value or a broken action is a blocker however good the screen looks. A remaining tell is a finding. A matter of taste inside the direction brief is not reported at all.

Every claim needs something you inspected: a layer, a line, a screenshot region, a computed ratio. A check you could not run is `Not verified`, never a pass.

Work from the source, the result and the contract themselves. Open them again. Do not verify from a description of what was done.

## 1. Content parity

Go through the contract row by row against the result.

| Check | Blocker when |
| --- | --- |
| Every row has a ledger entry | A row has none |
| `keep`, `restyle`, `merge`, `move` rows: the value appears in the result, character for character | A digit, unit, name or word differs |
| `relabel` rows: an interface label, not data, and the old label is recorded | Data or user content was reworded |
| `demote` rows: the named entry point exists in the result | It is not there |
| `cut` rows: the element passes the cutting test in the contract | Live data with no other home was cut |
| Nothing new: every value in the result is in the contract, is computable from it, or is a marked placeholder | A plausible-looking invented value |
| Every action reaches the same destination | A handler, link or route is gone or changed |
| A visible label that was shortened still makes sense where it now sits, and keeps its full accessible name | `Start` with nothing nearby saying what starts |
| Every state the source has exists in the result | A loading, empty or error state was dropped |
| In `reskin` mode: no `move`, `relabel`, `demote` or `cut` at all | Any appears |

Compare the strings from layer data or code, not from the screenshots. Then read the result's screenshot once for anything on screen that is in neither list.

When the source is only a screenshot, the contract is itself a transcription. Audit it first: read the source image against the contract and report anything missed or misread, including icons, chart shapes and selected states. A `demote` whose destination cannot be seen in the source is reported as **Not verified**, and is a blocker only if nothing in the source points to that destination. Contract columns left as `unknown` are not failures. Columns dropped altogether are a finding.

For code, also read the removed side of the diff for lost handlers, `data-testid`, `id`, `aria-*`, `alt`, labels, semantic elements and conditional branches.

## 2. Does it still look generated

Re-run the first read, the squint test and the swap test from `unslop-diagnose` on the result, then scan for tells.

- **Old tells that survived.** Every tier 1 tell from the diagnosis must be gone. Tier 2 and 3 tells that remain are findings.
- **New tells introduced.** A restyle can swap one default for another: glass on everything, a sunset behind a spreadsheet, an overline on every label, a new ring. Report these the same way.
- **Only tidier.** Put the source and the result side by side at thumbnail size. If the result is the same screen with better spacing and calmer colors, on any kind of view, nothing is at full strength. That is a blocker, not a finding: the owner is `unslop-direction`, **Every view has one place at full strength**.
- **The premium bar.** Run the list in `unslop-principles`, **Correct is not finished**. Each line that is not done and has no reason from the product is a finding. Three or more is a blocker.
- **The swap test.** If the result would still work unchanged for a product in another category, the direction did not reach the signature or the atmosphere. That is a finding against `unslop-direction`.

## 3. Is it one design

Check the result against the direction brief:

| Check | Finding when |
| --- | --- |
| Every color traces to a role | A color with no role, or a leftover from the old palette |
| One accent hue: as the field, bleed or wash of one region, on the primary action and on at most one data highlight | A second accent hue, or the accent on more than four elements outside its region |
| At most two type families and five sizes | More |
| Large text is light, small text is not | 40px or more at 600 or heavier outside the Graphic direction, or under 18px below 400 |
| One radius family and one corner language | More than three radius values, or pills and circles mixed with rounded rectangles |
| Gaps on the spacing scale, same relationship same gap | Off-scale or inconsistent gaps |
| One way of separating surfaces | Stroke, fill and shadow together, or mixed methods |
| One focal point | Two regions competing, or the focal point boxed in a card |
| The treatment fits the brief's kind of screen | A gradient, glass or oversized figure on a work view, form or table. Rows, columns or fields thinned out for looks |
| The brief's five dials are visible in the result | A dial the result ignores or contradicts |
| The tests in `unslop-principles` pass | Any that fails, named by its number |

## 4. Can it be read and used

- **Contrast.** Compute the ratio for every text element against the lightest and darkest region it sits over. 4.5:1 for body and labels, 3:1 for text at 24px and up and for meaningful icons and chart marks. Text on glass is measured against the composited surface. A failing pair is a blocker for primary content and a finding for tertiary marks.
- **Color is not the only signal.** Selected state, direction of change and status each have a shape, icon or word as well.
- **Long content.** Put a long value in every slot that takes data: a 30-character name, the widest time or amount the field allows, a five-digit number in a stat, a 60-character title in a table cell. Then lengthen the interface labels by half, as a translation would, paying most attention to any label beside an element that overlaps its container, such as a button placed over a group. Nothing clips, overlaps or pushes the focal point off its axis.
- **Narrow and large.** The narrowest supported width, 320px on the web, and large text settings. Controls stay reachable and inside the margins. A fixed-size mock built from a screenshot has no narrow layout to test: say so under **Not verified** instead of failing it.
- **Text on glass.** Model the surface as its fill composited over the local background and ignore blur and saturation, which change the result by a few percent. Where a render is available, sample the surface's actual color as a cross-check.
- **Targets.** 44 by 44 for every control on touch screens, including small chips that act. 24 by 24 with clearance for pointer-only interfaces.
- **States.** Every state in the contract still exists in the new style, and focus is visible on every control.
- **The primary action** is visible without scrolling on a phone and is not covered by fixed navigation.

## 5. Is the file left in good order

For Figma: the source frame is unchanged, the copy is named and placed clear of others, text is still text, instances are attached, fills are bound to variables, layers are named, nothing is hidden instead of deleted.

For a build from a screenshot there is no source file and no diff. Check the built file instead: valid markup, no unused tokens, no literal colors that repeat a token, no duplicated or hidden elements.

For code: the diff touches presentation only, no unapproved dependency, tokens used in place of literals, no dead styles or imports, typecheck, lint and tests pass.

## What it returns

```markdown
## Verification: <screen>

Verdict: Ship | Fix first

Content parity: <n> of <n> contract rows accounted for. <blockers, or "none">

| Severity | Finding | Where | Evidence | Owner |
| --- | --- | --- | --- | --- |
| Blocker | Invoice total changed | Invoice table, row 3 | Contract `$1,240.50`, result `$1,240.00` | `unslop` contract |
| Blocker | Label contrast fails | `Due date` label over the bright band of the header | 2.3:1, needs 4.5:1 | `unslop-color` |
| Finding | Saturated pill behind the selected item | Sidebar | 36px accent circle behind the selected icon | `unslop-navigation` |

Measured: <pairs with ratios>
Not verified: <checks that could not be run, and why>
```

`Ship` means no blockers, every tier 1 tell gone, nothing in the result that the brief's **Avoid** line names, and the brief's `Strength:` line visible in the result. A correct and plain result is `Fix first`. `Fix first` otherwise. A pattern from the catalog that the brief's atmosphere or subject explains, such as a violet evening sky in a weather app, is not a surviving tell: say so in one line and move on.

Counting rules, so two readers get the same answer: a unit span sized relative to its figure does not count as a type size. Fully round shapes count as a corner language, checked separately: a view mixes pills or circles with rounded rectangles only where a shape is round by nature, such as a status dot. The device frame does not count as radius values. The hero's own marks may carry the accent and do not count as the one data highlight. Order rows with blockers first, then findings by how visible they are. Cap findings at ten. Never cap blockers.

## Before you finish

| You notice | Fix |
| --- | --- |
| Parity checked by comparing two screenshots by eye | Compare the strings from layer data or code |
| A `Ship` verdict with unmeasured contrast on a gradient or glass | Measure it, or change the verdict's basis to **Not verified** and say so |
| A finding that says the result is "not premium enough" | Name the tell or the brief dial it misses, or drop it |
| A finding against a choice the brief made deliberately | Drop it. Disagreeing with the direction is not verification |
| An edit made to fix something | Revert it and report the finding |
| Only the default state was looked at | Check each state the contract lists |
| The source was not reopened | Open it and compare again |
| New tells not scanned for | Run the scan on the result as if it were a fresh screen |
