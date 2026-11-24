---
name: unslop-layout
description: Gives a generic interface a clear order. Finds the one focal point of a view, cuts or demotes what does not serve it, breaks uniform card grids, and puts every gap on one spacing scale. Works on dashboards, tables, forms, landing pages, feeds and mobile screens. Use when a screen feels like a template, has equal-weight sections, too many cards, no clear focal point or inconsistent spacing, or as the layout pass of unslop.
---

# Layout

This skill restructures a view so one thing leads and the rest supports it. It runs first, because every later pass paints whatever structure this one leaves.

What may be cut, and how cuts are recorded, belongs to `unslop`'s content contract. Fills, borders and radius belong to `unslop-surfaces`. The form of figures and charts belongs to `unslop-dataviz`. Navigation structure and labels belong to `unslop-navigation`. Sizes and weights of text belong to `unslop-typography`.

## Structure is judged by eye, spacing by number

Which element leads and what leaves are judgment calls, made from the direction brief. Make them and say why.

Spacing is not. Every gap sits on the scale below, and the same relationship gets the same gap everywhere. A gap of 14 between two cards and 16 between two others is a defect whatever the screen looks like.

Use the project's layout primitives, breakpoints and spacing tokens where it has them. The numbers here apply where it has none.

In `reskin` mode, nothing is cut, moved or reordered. Apply only the spacing, alignment and margin rules.

## Every view has one focal point

The brief names the view's job as a question. One region answers it. That region is the focal point, and nothing else competes with it. What it is depends on the kind of screen the brief names:

| Kind | The focal point is | It leads by |
| --- | --- | --- |
| Focus | One figure, object or statement | Size and empty space. 35 to 50 percent of the first viewport on a phone, the upper half on desktop |
| Work | The primary table, list, chart or canvas | Area. It gets the most room and the widest column, and it starts above the fold |
| Form | The column of fields, ending in one primary action | A single column with nothing beside it that is not help for the field in focus |
| Collection | The items | Uninterrupted repetition. Filters and headers stay thin |
| Marketing | The headline and one call to action | Type size, with the product shown directly under or beside it |
| Flow | The single question or task of this step | Being alone on the screen |
| Overlay | The decision: a title, what happens, the action | Nothing else being present |

The squint test checks it: blur the view or shrink it to a thumbnail, and one region clearly dominates, with two or three quieter groups around it. Four regions of equal weight is the template look.

The focal point is not in a card like the others. A figure, a table or a headline inside the same bordered box as everything else is one more tile. The exception is the full-strength object `unslop-direction` names on a focus or marketing view: there the focal point may be an object in its own right, such as a balance on a card, as long as nothing else on the view shares its treatment.

A figure and the actions taken on it belong together. Put the two or four actions that act on the focal figure inside or directly against its object, so the figure and what you do with it read as one thing.

## Summary rows do not lead

The usual generated dashboard opens with a row of four stat cards, then two charts side by side, then a table. Nothing leads, and the row of cards takes the best position on the screen for four numbers.

- Decide which one or two numbers answer the view's question and give them the focal position, large. The others become a compact line of label and value pairs, in the page header or beside the main chart.
- Two charts of equal size side by side: make the one that answers the question wide, and move the other below it or into a narrower column.
- The table that people actually work in moves up. A summary that pushes the working surface below the fold has the order backwards.

## Cut until the focal point is obvious

Go through the content contract row by row and give each a disposition. The usual candidates:

| Element | Usual disposition |
| --- | --- |
| A greeting or welcome line used as the headline | Keep, at caption size, or cut when the view's title already orients |
| A hardcoded tip, quote, generic insight or "Did you know" | Cut. It is filler |
| A subtitle under every heading that restates the heading | Cut |
| A secondary chart that a dedicated view already shows in full | Demote to that view |
| A value shown twice, such as in a stat card and again in a table footer | Merge into one |
| A section title above a group that is obvious without it | Cut the title, keep the group |
| A "View all" link beside every section | Keep it only where a full view exists and is not already in the navigation |
| Three feature cards that repeat the headline's claim in other words | Merge into the copy, or keep the one with a concrete fact |
| A decorative illustration, badge or icon row that carries no information | Cut |
| Filters, a date range, a search field, an avatar | Keep, small, in the header or a toolbar |

Follow the cutting test in the contract. Data with no other home is demoted, never cut. Record every decision in the ledger.

Density is not clutter. A work screen with forty rows and twelve columns is doing its job. Do not thin out a dense tool to make it look calm: remove what is redundant, keep what is used.

## Break the uniform grid

Identical cards in an even grid is the layout a model reaches for first: four stat tiles, three feature cards, six equal dashboard panels. Keep the content and give the arrangement a shape:

- **Demote the set to one quiet group.** Remove the cards' individual weight so the values read as one block of label and value pairs, not several small headlines.
- **Let one item be bigger** when one matters more. Unequal sizes say which.
- **Turn a grid into a row, a list or a table** when the items are a sequence, a ranking or records with the same fields. Six cards with the same four fields are a six-row table.
- **Give the grid a center** when the view has one primary action and the set is small: placing the action where the tiles meet turns a grid into a composition. The action then overlaps the tiles' inner corners, so pad each tile on its inner side by enough that a label which grows or wraps cannot run under it.
- **Alternate the composition** on a marketing page: a section with the product on one side, a full-width figure, a short list. Three centered sections of heading, subtitle and three cards in a row is the same block three times.

A grid stays a grid when the items really are equal and the user compares them: products, photos, files, plans.

Do not add items to fill a grid. Three values are three values.

## One spacing scale

Use the project's spacing tokens when it has them. Otherwise use this scale and nothing between its steps:

`4, 8, 12, 16, 24, 32, 48, 64, 96`

| Relationship | Gap |
| --- | --- |
| Icon to its label, value to its unit | 4 to 8 |
| Label to its field or value, lines within one item | 4 to 8 |
| Padding inside a card, tile or panel | 16 or 20 on a phone, 20 or 24 on desktop. The same on every sibling |
| Table cell padding | 12 to 16 horizontal, 8 to 12 vertical. 8 vertical is a dense table, 12 a comfortable one |
| Between sibling items in a group | 8 or 12 |
| Between fields in a form | 16 to 24 |
| Between groups | 24 or 32, at least twice the gap within a group |
| Between sections of a page | 48 to 64 in a product view, 96 or more on a marketing page |
| Around a focal figure or headline | 32 to 48 on a phone, 48 to 96 on desktop |
| Page side margin | 20 or 24 on a phone, never under 16. 24 to 48 on desktop |

The same relationship takes the same value across the whole view. If two card gaps differ, one of them is wrong.

## Width has a limit

- Running text holds 45 to 75 characters a line. A paragraph that spans a 1400px container is unreadable whatever its styling.
- A form column is 320 to 560 wide. Wider fields do not make a form easier.
- A centered content column on desktop is 1100 to 1280 at most, with the background running to the edges.
- Tables and canvases are the exception. They take the width they are given.

## One axis

Pick the alignment the composition hangs on and hold it. A focus view with a single centered figure can be centered. Lists, forms, tables and nearly every work view align to the leading edge. Do not mix a centered heading with left-aligned content below it.

- Labels, fields and the action of a form share one leading edge.
- Numbers in a column align right, on tabular figures. Text aligns to the leading edge. Column headers align with their column.
- A marketing section is centered only when its text is short: a headline and one or two lines. Longer copy aligns to the leading edge.

## The primary action sits where it is expected

One primary action per view. Where it goes depends on the kind of screen:

| Kind | Position |
| --- | --- |
| Phone, any kind | In the lower half, clear of the navigation bar. Consider whether it can live inside the composition and not as a full-width bar |
| Form | At the end of the fields, on the leading edge of the column, primary first |
| Work view | In the page header, on the trailing side, level with the title |
| Overlay | In the footer of the dialog, following the platform's order |
| Marketing | Directly under the headline, and once more at the end of the page |

Its label and its restyling belong to `unslop-navigation` and `unslop-surfaces`.

## The top carries context, not content

The top of a view orients: a title or a date, a way back, the controls that scope what is shown, the account. One row on a phone. On desktop, one page header with the title leading and actions trailing. No title that repeats the selected navigation item, and no welcome banner above the work.

## It holds at other widths

A restyle that only works at the width of the source is half done.

- Keep the expanded layout until the content stops fitting, then collapse. Breakpoints come from the content.
- A sidebar collapses to icons or a menu before the main column drops under about 600.
- Multi-column groups stack in reading order. The focal point stays first.
- Wide tables scroll inside their own container with the first column pinned, or drop their least important columns. They do not shrink their text.
- Give text containers a minimum height, not a fixed one, so a longer label wraps without clipping.

## Before you finish

| You notice | Fix |
| --- | --- |
| Blurred, the view shows three or more regions of equal weight | Pick the focal point and demote the rest |
| The focal figure, table or headline has a border, a fill or a card around it | Remove the container and give it space |
| A row of equal stat cards above the content that answers the view's question | Promote one or two figures, fold the rest into a compact line |
| The working table or list starts below the fold on desktop | Move it up and shrink what is above it |
| The largest text on the view is a greeting | Shrink it to caption size or cut it |
| Six cards with the same fields | A table or a list |
| Three sections in a row built the same way: heading, subtitle, three cards | Vary the composition, or merge sections |
| A gap value that is not on the scale, such as 10, 14 or 18 | Move it to the nearest step |
| The same relationship with two different gaps | Use one |
| The gap between groups is less than twice the gap inside them | Raise it to 24 or more |
| Different padding inside sibling cards | One value for all |
| A paragraph wider than 75 characters, or a form field wider than 560 | Limit the column |
| A centered heading over left-aligned content | One axis |
| Numbers in a column aligned left or centered | Align right |
| A contract row gone from the view with no ledger entry | Restore it or record it |
| A tile, stat or section added to balance the layout | Remove it. Nothing is invented |
| Rows, columns or fields removed from a work view to make it look calmer | Restore them. Cut only what is redundant |
| Content moved or cut in `reskin` mode | Put it back |
| Text or controls closer than 16 to the screen edge | Bring them inside the margin |
| An element placed over a group, with text in the group able to reach it when a label grows | Reserve the clearance as padding inside the group |
| A fixed height on a box that holds text | A minimum height |
| A row of equal labeled buttons whose longest label fills its button | Give it room for a third more: fewer columns, smaller gaps, or the label under a wider cell |
| A focal figure in one place and its actions in another group | Bring the actions into or against the figure's object |
