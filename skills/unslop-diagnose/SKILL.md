---
name: unslop-diagnose
description: Finds what makes any interface look AI-generated - a dashboard, a landing page, a form, a table or a mobile screen. Scans a Figma frame, code or a screenshot against a catalog of tells - default palettes, boxed icons, uniform card grids, stat-card rows, generic charts, one-weight type - and returns them ranked with the skill that fixes each. Read-only. Use when asked why a design looks generic, templated or AI-made, or as the first step of unslop.
---

# Diagnose

This skill names the specific patterns that make a screen read as machine-made and ranks them by how much of that impression each one carries. It reads and reports. It changes nothing and proposes no redesign.

The fixes belong to the other skills: `unslop-layout`, `unslop-surfaces`, `unslop-dataviz`, `unslop-typography`, `unslop-color` and `unslop-navigation`. The fundamentals a tell usually breaks are in `unslop-principles`. The full pipeline is `unslop`.

## A tell is a default nobody chose

Slop is not ugliness. An AI-generated screen is usually tidy, aligned and legible. What gives it away is that every decision is the most common one: the most common palette, the most common chart, the most common card. Nothing on the screen could only belong to this product.

So the test for a tell has two parts. The pattern is present, **and** nothing about the product explains it. A donut that shows a real part of a whole is a chart. A donut around a score, because scores get donuts, is a tell. A purple brand that has been purple for ten years is a brand. Indigo because the model reached for indigo is a tell.

Report a pattern as a tell only when both parts hold. When a documented brand or design-system decision explains it, leave it out.

## Scan in three tiers

Rank by how much of the generic look a tell carries, not by how easy it is to fix.

- **Tier 1, identity.** The palette, the dominant element and the typeface. A viewer decides "AI-made" from these in under a second. Fixing only these already changes what the screen is.
- **Tier 2, structure.** Equal-weight sections, everything in a card, uniform grids, a row of stat cards above everything, too many destinations. These make the screen feel like a template.
- **Tier 3, detail.** Borders, icon tiles, pills, glows, radius and spacing drift. Each is small. Together they are the texture of the default.

The catalog, with how to detect each tell in code and in Figma, is in [slop-tells.md](slop-tells.md).

## How to look

1. **Look at the render first.** Take or open a screenshot before reading any code or layer tree. Note what you see in the first second: the dominant color, the largest element, the typeface. That first read is the tier 1 evidence.
2. **Squint.** Blur the screenshot or view it at thumbnail size. Count how many regions have the same visual weight. Four or more equal blocks with no clear largest one is the structure tell.
3. **Do the swap test.** Imagine the product name, the labels and the numbers replaced with another category's: a CRM in place of a fitness app, a payroll tool in place of an analytics one. If the screen would work unchanged, write down which elements made that possible. Those are the tells.
4. **Name the kind of screen**: focus, work, form, collection, marketing, flow or overlay, as defined in `unslop-direction`. The catalog has tells for each, and a pattern that is a tell on one kind is correct on another: a dense table is not a tell on a work view.
5. **Then read the source** for the detection patterns in the catalog. Code and layer data confirm what you saw and find what you missed, such as five font sizes within 3px of each other.

## What it returns

```markdown
## Diagnosis: <screen>

Kind: <focus, work, form, collection, marketing, flow or overlay>
First read: <one sentence on what the screen looks like at a glance>
Swap test: <would it work for another product unchanged, and why>

| Tier | Tell | Where | Evidence | Owner |
| --- | --- | --- | --- | --- |
| 1 | Default indigo-violet palette | Whole screen | `#6366F1` to `#8B5CF6` gradient on the button, `#0F172A` background, no brand doc | `unslop-color` |
| 1 | Stat-card row leads | Top of the page | Four equal cards above the invoice table the view exists for | `unslop-layout` |
| 2 | Everything in a card | Stats, both charts, the table | The same `rounded-xl border bg-white` wrapper on six sections | `unslop-layout` |
| 3 | Boxed icons | Four stat cards | 40px tinted rounded squares behind 20px icons, four different hues | `unslop-surfaces` |

Not tells here: <patterns that are present but explained by the brand or the content>
Not checked: <what you could not inspect>
```

Cite a location for every row: a layer name, a `file:line`, or a region of the screenshot. One row per tell, however many times it repeats. List every tier 1 tell. Cap tiers 2 and 3 at the ten that matter most.

## Before you finish

| You notice | Fix |
| --- | --- |
| A finding that says "looks generic" with no named pattern | Name the pattern from the catalog or drop the row |
| A brand color or documented convention reported as a tell | Move it to **Not tells here** |
| Only color findings in the table | Run the squint and swap tests. Palette is one tell of many |
| Density reported as a tell on a work view | Remove the row. Dense and even is correct there |
| No `Kind:` line in the diagnosis | Name the kind of screen |
| A row whose evidence is a hex code seen in a screenshot | Read the value from the source, or say it is estimated |
| A redesign proposal in the report | Remove it. Direction belongs to `unslop-direction` |
| Twenty tier 3 rows | Keep the ten most visible and say how many were left out |
