---
name: unslop-typography
description: Gives a generic screen a typographic voice. Replaces the default typeface with one that has character, makes large text lighter, reduces the number of sizes and weights, and builds hierarchy from size and tone. Use when everything is Inter or Roboto semibold, text feels heavy or flat, there are too many font sizes, or as the type pass of unslop.
---

# Typography

This skill chooses the typeface and sets the scale, weights and tones of text so the screen has a voice and a clear order of reading. It changes how text looks and never what it says.

How a figure's value and unit are composed belongs to `unslop-dataviz`. Text colors and contrast belong to `unslop-color`. Rewording labels belongs to `unslop-navigation`. Loading font files into a project belongs to `unslop-code`.

## The face is a judgment, the numbers are not

Choosing a typeface is taste, guided by the brief's type voice. Choose one and commit.

The rest is exact: at most two families, at most five sizes, weights by size as given below, three text tones. A screen with seven sizes is wrong whichever face it uses.

A documented brand typeface is fixed. Keep it and apply only the scale, weight and tone rules. Never replace a brand face.

## A face with a voice

Inter, Roboto, Poppins and the system font are fine typefaces. They are also what every generated screen uses, so they carry no information about this product. When nothing is fixed, pick a face that fits the brief's voice:

| Voice in the brief | Look for | Starting points |
| --- | --- | --- |
| Soft, calm, friendly | Rounded terminals, open shapes, a real light weight | Manrope, Outfit, Figtree, Urbanist, Plus Jakarta Sans |
| Precise, technical | A tight grotesque with a matching mono | Geist with Geist Mono, IBM Plex Sans with IBM Plex Mono, Hanken Grotesk |
| Editorial, considered | A serif with contrast for display, a quiet sans for interface | Instrument Serif, Fraunces or Newsreader for display with a neutral sans |
| Confident, graphic | A display face with strong shapes for one line | Bricolage Grotesque, Unbounded, Archivo |
| Neutral with a little warmth | A humanist sans | DM Sans, Onest, Albert Sans |

These are open-licensed families. Before committing, check three things: the family is available to the project, it ships the weights you plan to use, and it has the glyphs the content needs, including any non-Latin script in the contract. More pairings and what each needs are in [font-pairings.md](font-pairings.md).

Two families at most: one for display and figures, one for interface text, or one family for everything. A mono counts as a third only when figures need it.

A display face earns its place by contrast with the interface face: a serif for the large figures and headlines over a plain sans for everything else is the most reliable pairing. Use it on the largest text only, the focal figure and at most one other level, and never for labels or controls. Before committing, render its numerals: they should be lining figures of even width, and a figure that changes in place needs a tabular set or a fixed-width container.

## Big text gets lighter

Generated screens set everything important in semibold or bold. At large sizes that reads as shouting, and it is the main reason a screen feels heavy. Weight goes down as size goes up:

| Size | Weight |
| --- | --- |
| 40px and above: hero figures, display | 300, or 400 if the family has no 300 or the text sits on a busy background |
| 24 to 39px: titles | 400 to 500 |
| 16 to 23px: headings, large values | 500 |
| 13 to 15px: body, labels, values in tiles | 400, with 500 for emphasis |
| 11 to 12px: captions, overlines | 500 |

Below 18px never go under 400. Thin weights at small sizes break up on screen.

Light text needs enough contrast behind it. Over a gradient or image, step the hero up to 400 before its strokes start to disappear.

The Graphic direction is the exception: its one display line stays heavy by design.

## Few sizes, wide steps

Use at most five sizes in a view, each at least 1.2 times the one below, with a bigger jump to the largest. The set depends on the kind of screen the brief names:

| Role | Focus, phone | Work and form, desktop | Marketing | Line height | Tracking |
| --- | --- | --- | --- | --- | --- |
| Display: main figure or headline | 56 to 72 | 28 to 36, only where one figure leads | 56 to 96 | 1.0 to 1.1 | -0.02em, to -0.03em above 72 |
| Title | 24 to 28 | 20 to 24 | 32 to 40 | 1.2 | -0.01em |
| Heading or large value | 17 to 20 | 15 to 16, medium weight | 20 to 24 | 1.3 | 0 |
| Body, labels, table cells | 14 to 15 | 13 to 14 | 17 to 20 | 1.4 to 1.6 | 0 |
| Caption and overline | 11 to 12 | 11 to 12 | 13 to 14 | 1.3 | 0 for sentence case, 0.06 to 0.08em for uppercase |

A work view is set small and even. Its hierarchy comes from tone, weight and position, not from big headings: a 32px title above a 13px table is a marketing habit in the wrong place. A marketing page is the opposite: few words, large, with long-form body at 17 and up.

Running text holds 45 to 75 characters a line at a line height of 1.5 to 1.6. Interface text is tighter, 1.3 to 1.45.

Map every text element to one of the roles. Sizes that sit between two roles, such as 13 and 15 used for the same kind of label, collapse into one. A unit span sized relative to its figure is part of that figure and does not count as a size. Give small units one of the existing sizes instead of a ratio that lands between two.

Use the project's type scale when it has one. Drop to the nearest existing step and do not add steps.

## Hierarchy from tone before weight

Three tones of the text color do most of the work that bold was doing:

| Tone | Strength | Use |
| --- | --- | --- |
| Primary | 100 percent | Values, titles, the identifying column of a table |
| Secondary | About 65 to 70 percent | Labels, supporting text, table headers |
| Tertiary | About 45 to 50 percent | Units inside a figure, disabled, placeholder |

These strengths are for flat backgrounds. Over a gradient or glass the secondary tone usually has to be stronger, around 80 to 85 percent, and the exact value comes from measurement. Set the tones as colors, not as opacity on the text element, when text sits over a gradient, so they can be measured. `unslop-color` owns the values and their contrast. Small tertiary text over a busy background usually fails, so keep tertiary for large units and non-essential marks.

A label and its value differ by tone and size. They do not also need different weights.

On a work view, where sizes barely differ, weight does more: medium for the one thing that identifies a row or a section, regular for everything else. Two weights, used for one distinction each.

## One overline style, used once or twice

A small uppercase label with wide tracking is a strong device, and a generated screen puts it on everything. Keep one overline style and use it for one kind of thing, such as the label of the main figure or the eyebrow above a marketing headline. Other labels are sentence case at caption or body size.

Set uppercase with `text-transform`, or Figma's case setting, never by retyping the string. The contract string stays as it was.

## Details that separate set type from default type

- **Tabular figures** on values that change or align in columns.
- **Negative tracking only on large text.** -0.02em at 40px and up, -0.01em at 24 and up, none below.
- **Sentence case** for labels and buttons unless the product's voice documents otherwise. Uppercase or lowercase set with a transform is styling. Turning `Deep Sleep` into `Deep sleep` edits the string, so it is a `relabel` and belongs to `unslop-navigation`: allowed in `full` mode, recorded in the ledger, never applied to data.
- **No gradient text.** A figure filled with the accent gradient is a tell. Solid color.
- **No emoji standing in for icons.** Replace an emoji bullet with an icon from the screen's set, or with nothing. Emoji inside user-written content stay.
- **Balance short headings** with `text-wrap: balance`. Never center text that runs past two lines.
- **No dot separators.** A middle dot or bullet between short facts on one line, such as `Instant · Free · Secure`, is a default way to avoid deciding how the facts relate. Give each fact its own item with a gap of 12 to 16 between them and an icon where one helps, stack them as a short list, or put them in separate cells. A dot stays only inside one compound value, such as a time and a date in a table cell, and in breadcrumbs or metadata the product's own style documents. Removing the dot is styling, not a relabel: each fact's string is unchanged.
- **Real punctuation** in interface strings you are allowed to touch: `…` for three dots, an en dash in ranges. Data values are never retyped.

## Before you finish

| You notice | Fix |
| --- | --- |
| Inter, Roboto, Poppins or a system stack on every layer, with no brand doc behind it | Choose a face from the brief's voice |
| A brand typeface replaced | Restore it and apply the scale and weight rules only |
| Text at 40px or more set in 600 or 700, outside the Graphic direction | 300 or 400 |
| Text under 18px at 300 or lighter | 400 |
| A weight the chosen family does not ship | Pick a weight it has, or another family |
| More than five sizes on the screen | Collapse to the five roles |
| A title of 28px or more on a dense work view | 20 to 24 |
| Body copy on a marketing page under 16px, or lines past 75 characters | 17 and up, in a limited column |
| Three or more weights in one view | Two, each with one job |
| Two sizes 1 to 2px apart used for the same kind of text | One size |
| More than two families | Reduce to two |
| A display face on labels, buttons or body text | The interface face. Display is for the largest text only |
| Old-style or uneven numerals in an amount or a column | Lining, tabular figures, or another face |
| Most text at semibold | Regular, with hierarchy from size and tone |
| Uppercase tracked labels on every group | Keep one use, sentence case for the rest |
| Letter spacing below zero on text under 24px | Remove it |
| A string retyped to change its case | Restore the string and use a case transform |
| Gradient fill on text | Solid color |
| An emoji used as a bullet or an icon | An icon from the set, or nothing |
| `·` or `•` between short facts on one line | Separate items with a gap, a stacked list, or separate cells |
| Secondary or tertiary text set with `opacity` over a gradient | A solid color token, measured |
| A typeface with no glyphs for a script the content uses | Choose one that covers it |
