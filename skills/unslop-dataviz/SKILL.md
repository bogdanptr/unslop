---
name: unslop-dataviz
description: Restyles figures, charts and tables on a generic interface. Picks chart forms that fit the comparison, gives a main figure a form that belongs to the product instead of a ring or donut, sets how numbers and units are styled, cleans up tables and strips chart junk. Use when a dashboard is stat cards and library-default charts, a main figure is a ring or donut, tables are hard to scan, or as the figures pass of unslop.
---

# Figures, charts and tables

This skill decides how data is drawn: the form of each chart, the styling of numbers, the rhythm of tables. It changes how data looks and never what the data is.

Which element is the focal point belongs to `unslop-layout`. The typeface and weights belong to `unslop-typography`. Chart colors belong to `unslop-color`. What may be cut belongs to `unslop`'s content contract.

A view with no figures, charts or tables skips this pass. Say so in one line.

## Every mark is a value from the contract

A chart is a claim about data. The form is open to judgment: pick the one that fits. The marks are not: each one that looks like data must map to a value in the content contract, and lengths, angles and positions must be proportional to those values.

Decoration is allowed when it cannot be mistaken for data. A row of dots that looks like a scale but measures nothing is a fake chart.

In `reskin` mode, keep each chart's form and apply only the number styling, table rules and junk removal below.

## The form follows the comparison

Generated charts are whatever the library renders first. Choose the form from what the reader compares:

| The reader compares | Use | Not |
| --- | --- | --- |
| A value over time | A line. An area only for a single series whose volume matters | Bars for a long continuous series |
| Values across a few categories | Horizontal bars, sorted, labeled directly | A pie, a donut, vertical bars with rotated labels |
| Parts of one whole, 2 to 4 parts | One segmented bar | A donut with a legend |
| One value against a target or a limit | A bar with the target marked, or the figure with the limit beside it | A ring, a gauge |
| One value against its usual range | A range strip with a marker | A colored badge |
| Two measures of the same things | A scatter, or a table with both columns | Two charts side by side |
| Many values that have to be read exactly | A table | Any chart |

A number with no comparison is a number. Set it as text. A sparkline, a ring or a progress bar beside it has to add a fact the number does not carry.

## A main figure takes its form from the subject

On a focus view the brief may name a figure as the signature. The default for any such figure is a ring around a number, which says "this is a score" and nothing else. Work through four questions:

1. **What is the datum?** Its value, its unit, what it is a part of, the period it covers.
2. **What is the story?** One of: progress toward a goal, a span between two moments, change over time, a level within a range, parts of a whole, a position on a route, a comparison with usual.
3. **What shape does the subject already have?** The brief names what the product is about. That subject usually has a shape of its own.
4. **Does the data exist to draw it?** List what the new form needs. Anything not in the contract is missing data.

| Subject | Its own shape | Instead of |
| --- | --- | --- |
| A shift, a session or a trip | A span from its start to its end, with the two times at the ends | A score ring |
| A day's activity | The day as a horizontal strip with active stretches filled | Three nested rings |
| A monthly budget | A bar that drains across the month, with today marked | A donut of categories |
| A run or ride | The route line, or its elevation profile | A distance stat card |
| A savings goal | A vessel that fills | A percentage ring |
| Portfolio or revenue | The line itself, large, with the figure on it | A number in a card with a tiny sparkline |
| Storage or quota | A segmented bar, one segment per kind | A donut |
| A delivery or a project | The route or the timeline with the current position | A percent-complete ring |
| Uptime or build health | A strip of days or runs, one mark each | A green percentage |

More swaps, and how to draw them, are in [chart-swaps.md](chart-swaps.md).

A ring stays when the subject is circular: a timer, a clock, a cycle that returns to its start.

This section applies to one figure per product. A work view with eight charts does not get eight inventions. It gets the comparison table above, applied consistently.

## When the new form needs data the screen does not have

A span needs a start and an end. A target bar needs a target. If the contract has only the value, the rest is not known.

- If the value is **computable** from contract values, compute it and show it.
- If the value **exists in the data model** but was not on the screen, such as a field on the same object, use it and add it to the contract as a new row marked `added from model`.
- Otherwise draw the form with a **marked placeholder**, such as `--:--`, list it under **Needs data** in the report and name the field it expects.

Never fill the gap with a plausible number. A made-up `11:24 PM` looks exactly like a real one.

## Numbers lead, units step back

- **Value** in the primary tone. A large figure is light in weight. Sizes and weights come from `unslop-typography`.
- **Unit** attached to its value, smaller and in a lighter tone, on the same baseline. In a large figure the unit is 50 to 60 percent of the value's size. `1h 24m` is four spans: `1`, `h`, `24`, `m`. A currency symbol and the decimals of a large amount step back the same way.
- **Label** above or below at caption size, in the secondary tone. One label style for every figure on the view.
- **Tabular figures** on anything that updates or sits in a column.
- **Consistent precision.** Every value of one kind shows the same number of decimals. The contract value is what is shown: restyle its parts, never round or reformat it.

The split is styling only. The string stays whole to a screen reader and in the contract.

## Deltas and status are quiet text

A comparison such as `24 min vs avg` or `+12.4%` does not need a colored pill.

- Set it as plain text or a small neutral chip in the secondary tone, with a simple arrow for direction.
- Use color only when direction is the point and the meaning is unambiguous, and then on the arrow or the text, not as a tinted background. Always keep the arrow, a sign or a word, so color is never the only signal.
- A status in a table is a small dot or plain text in the status color, not a filled badge in every row. Reserve a filled badge for the one state that needs action.

## Supporting stats are label and value

A group of secondary values shows label and value and nothing else:

- Label at caption size in the secondary tone, value at a medium size in the primary tone. No ring, bar or sparkline per item unless it adds a fact.
- One optional icon per item, bare, following `unslop-surfaces`. On a work view, usually none.
- The same structure for every item in the group.

## Tables are set, not boxed

A table is the densest data display there is, and a generated one is a grid of borders.

- **Rules, not boxes.** One hairline under the header and between rows, or no row lines and 8 to 12 of row padding. No vertical lines, no outer border, no zebra striping together with row lines.
- **Alignment by type.** Text to the leading edge, numbers to the right on tabular figures, dates in one format. Headers align with their column.
- **Header is quiet.** Caption size, secondary tone, sentence case, no fill.
- **One primary column.** The identifying value of each row is in the primary tone at regular or medium weight. Everything else is regular in the secondary or primary tone. No bold column of numbers.
- **Row actions on demand.** One trailing menu or hover actions, not three buttons in every row.
- **Hover and selection** are a quiet fill step, the same one the rest of the interface uses.
- **Empty and long values.** An empty cell shows a dash in the tertiary tone. A long value truncates with a way to read the whole.

## Strip the chart to its data

For every chart that stays:

- **Remove** the plot border, the background fill, gridlines that are not read, tick marks, and the legend when there are one or two series. Label the series directly.
- **Keep** one baseline and the axis labels needed to read a value. Three or four horizontal gridlines at most, as hairlines.
- **One highlight.** The current or selected point takes the accent. Everything else takes one muted tone from the palette.
- **Several series** take tones of one hue or a small set tuned to the same lightness and chroma, from `unslop-color`. Not the library's default rainbow.
- **Round data ends consistently**: bar ends at 2 to 4, or fully round when the bars are narrow. Line joins round.
- **Line weight** 1.5 to 2px for the main series, 1px for reference lines. Area fills fade toward the baseline.
- **Show the value** of the highlighted point as text. A chart with no readable number is decoration.
- **One chart style** across the product: the same axis treatment, the same tooltip, the same tones.

## Before you finish

| You notice | Fix |
| --- | --- |
| A pie or donut with more than four slices, or with a legend | Sorted horizontal bars, labeled directly |
| A ring, gauge or donut around a single number, and the subject is not a cycle | A bar against its target, or the subject's own shape |
| A sparkline, ring or progress bar beside a number that adds no fact | Remove it |
| A new figure that could sit unchanged in another category's product | It is still generic. Take the shape from the subject |
| A time, percentage or count on screen that is not in the contract | Compute it, source it from the model, or mark it as a placeholder |
| An arc, bar or fill whose length does not match its value | Make it proportional |
| Dots, ticks or segments that look like a scale but encode nothing | Remove them or make them unmistakably decorative |
| The unit at the same size and weight as the value in a large figure | Smaller, lighter tone |
| Values of one kind with different numbers of decimals | One precision, without changing a contract value |
| A green or red tinted pill around a delta | Plain text or a neutral chip with an arrow |
| Direction or status shown by color alone | Add the arrow, a sign or a word |
| A filled status badge in every table row | A dot or text. Fill only the state that needs action |
| A table with vertical lines, an outer border, or zebra striping plus row lines | Hairline row rules or padding alone |
| Numbers in a table aligned left or centered, or without tabular figures | Right-aligned, tabular |
| Two or more buttons repeated in every table row | One menu, or actions on hover |
| Gridlines, a plot border or a legend on a single-series chart | Remove them and label directly |
| The chart library's default colors | The palette's chart tones |
| Charts on one product with different axis and tooltip styles | One chart style |
| The chart form changed in `reskin` mode | Restore the form and keep the styling changes |
