---
name: unslop-color
description: Replaces a default palette with one that has a source, on any interface. Builds the background the direction calls for - usually a quiet tinted neutral, sometimes a gradient, material or image - derives every other color from it, tints the neutrals, keeps a single accent and measures text contrast on the result. Use when a screen is indigo on navy, gray on white, flat or lifeless, uses a different hue per metric, or as the color pass of unslop.
---

# Atmosphere and color

This skill builds the background the direction brief describes and derives the whole palette from it, so every color on the screen has the same origin. Then it measures whether text can still be read on the result.

The decision about what the atmosphere is belongs to `unslop-direction`. Fills, strokes and glass on surfaces belong to `unslop-surfaces`, which reads its colors from here. Chart marks belong to `unslop-dataviz`. Text tones are defined here and applied by `unslop-typography`.

## The source is chosen, the contrast is measured

Which atmosphere and which stop becomes the accent are judgments made from the brief.

Contrast is not. Body text needs 4.5:1 and large text 3:1 against what is actually behind it. Compute the ratio from the values. Never estimate it by eye, and never report a pair as passing that you did not measure.

Documented brand colors are fixed. Build the atmosphere around them. Semantic colors keep their meaning: an error stays in the red family whatever the palette.

## The background comes first

A generated screen picks a background from a short list of defaults and then adds an accent. Do it the other way round. Build the background from the brief's atmosphere, then take every other color from it.

The atmosphere stands for something in the product: the paper of a ledger, the dark of a cockpit, the sky the user wakes up to. It is one of four kinds, listed from the most common to the least:

| Kind | What it is | When |
| --- | --- | --- |
| A quiet neutral | One tinted neutral, flat, light or dark | Work views, forms, collections, most product interfaces. Still tinted, never pure gray |
| A material | A near-flat tone with warmth and a little grain: paper, stone, clay, ink | Documents, reading, tools, calm products |
| The content | A large blur of the current image or cover, or plain black or white behind it | Media, commerce, galleries |
| A phenomenon | A gradient of real light: dawn, dusk, night, deep water | Focus and marketing views whose subject is a time, a place or a state |

The brief's `Kind:` line limits the choice. A gradient or image behind a table, a form or an editor makes the work harder to read and is the new default to avoid.

Recipes with values for each are in [atmosphere.md](atmosphere.md).

## A neutral background is still designed

Most of the time the background is one tone. What separates a considered one from `gray-50` or `slate-900`:

- **A hue.** Chroma of 0.005 to 0.02 in OKLCH, in the direction of the accent or the brand, or its complement for a deliberate warm-cool contrast.
- **A lightness chosen, not inherited.** Light pages sit at 0.97 to 0.99, not pure white, unless the direction is paper-white with ink text. Dark pages sit at 0.14 to 0.20, not pure black, unless the content is media.
- **Two or three surface steps** from it, each 2 to 4 percent apart in lightness in the same hue: page, raised surface, hover or selected. On dark, raised surfaces get lighter. On light, they go to white or get slightly darker, one rule for the whole product.
- **No gradient for its own sake.** A flat tone, or one very slight vertical shift of 1 to 2 percent in lightness.

## A wash is the quietest gradient

A neutral page can carry a soft wash of the accent or brand hue where the view allows expression: focus, marketing and flow views, and the empty areas of a collection.

- The accent at 8 to 12 percent over the page color, as a solid computed value.
- It starts at the top edge, or behind the focal object, and fades to the plain page color within 40 to 50 percent of the first viewport. A radial shape wider than the screen fades more evenly than a linear one.
- One wash per view. It never sits behind a table, a form or running text.
- Text over it is measured like any other background. At this strength the page's text tones still pass.

## Build a gradient like real light

Only where the brief calls for a phenomenon:

- **3 or 4 stops**, mostly vertical. Real light changes from top to bottom, not corner to corner.
- **Adjacent hues.** Take stops that sit near each other on the wheel, or pass through a believable middle. Two opposite hues interpolated directly go gray halfway.
- **Interpolate in OKLCH or OKLAB**, `linear-gradient(in oklch, …)`, so the middle stays clean.
- **Lightness has a shape.** Decide where the bright band is and where it is dark, because that decides where text can go. A bright band behind the hero and a dark base under the controls is a good default.
- **Grain against banding.** Overlay 2 to 4 percent monochrome noise on large gradients.
- **No blobs.** Delete blurred accent circles and corner glows. They are the default decoration, and the atmosphere replaces them.

## Take every color from the background

Sample, do not invent. With the background built:

| Role | Take it from |
| --- | --- |
| `text-primary` on dark regions | A near-white tinted toward the background's warm stop: OKLCH lightness about 0.98, chroma 0.01 |
| `text-primary` on light regions | The background's darkest stop, darkened further: lightness 0.20 to 0.25, chroma 0.03 to 0.04 |
| `text-secondary`, `text-tertiary` | The primary text mixed toward what is behind it. About 68 and 48 percent strength on a flat background. Over a gradient or glass, set the strength by measurement: secondary often needs 80 to 85 percent to pass |
| `surface`, `surface-raised`, `surface-hover` | Steps of the background tone, 2 to 4 percent apart in lightness, or a translucent white or dark for glass |
| `accent` | The brightest or warmest stop, pushed to higher chroma |
| `on-accent` | The darkest stop, or the near-white, whichever measures higher against the accent |
| `hairline` | Primary text at 8 to 12 percent |
| `border-field` | Primary text at 12 to 20 percent, or whatever reaches 3:1 against the surface for an input's edge |
| Chart tones | One muted tone 10 to 15 percent from the background behind the chart, the accent for the highlight, and for several series a set at one lightness and chroma |

Never pure `#000` or `#FFF` on a colored background. The near-white and near-black above look cleaner because they share the scene's light.

## Neutrals are tinted

Gray with zero chroma looks dead beside any color. Every neutral carries the background's hue at low chroma, about 0.005 to 0.02 in OKLCH. On a quiet neutral atmosphere this tint is the whole palette, and it is what separates a considered gray screen from a default one.

## One accent, used for one thing

- **One accent hue.** It marks the primary action and, at most, the current or selected data point.
- **It covers little.** Roughly a tenth of the screen or less, and on a work view far less: the primary button, the focus ring, the selected state. If it is everywhere, nothing is primary.
- **Links are not automatically the accent.** In running text a link is the text color with an underline, or the accent where links are few.
- **No rainbow metrics.** Four stats in four hues with no meaning behind the hues become four stats in the text color. If the hues do encode categories, keep the categories and retune each to the palette's lightness and chroma.
- **Fill, not text.** The primary action is a solid accent fill. Accent-colored text on a neutral button reads as a link.

## A bleed joins the color to the page

The strongest way to place a brand color on a focus, marketing or flow view is to let it fill the top of the view and fade into the page:

- Full strength at the top edge, behind the status area, the header and the focal figure. It reaches the page color by 40 to 55 percent of the first viewport.
- Two or three stops in one hue: the brand color, a slightly lighter step of it, the page color. Interpolate in OKLCH so the fade does not gray out.
- Text and controls in the colored part follow **When the accent is a field**. Below the fade they follow the page's roles. Nothing with small text sits in the middle of the transition unless it is on its own surface.
- A content surface sits across the transition, so the color and the page are tied together by an object instead of a line.
- A bleed, a field on one object and a wash are three strengths of the same idea. A view uses one of them.

## Near-black is the second emphasis

With one accent, the second level of emphasis is the text color used as a fill: a near-black button, a near-black selected chip, a dark bar. It gives a second strong tone without a second hue.

- Use it for the control that matters second, and for selected states in filters and segmented controls.
- It does not count as an accent. It counts toward restraint: one or two near-black fills in a view.
- On a dark theme the roles swap, and the near-white does this job.

## When the accent is a field

On a view where `unslop-direction` names a full-strength object, the accent or brand color becomes that object's fill. The rules invert inside it:

| Role on the field | Value |
| --- | --- |
| Primary text | The page's near-white, or the near-black on a light brand color, whichever measures higher |
| Secondary text | That text color mixed toward the field, as a solid: start at 75 to 80 percent and measure. It needs 4.5:1 against the field |
| Quiet controls on the field | The field shifted one step toward the text color, about 12 to 16 percent, as a solid fill |
| The primary action on the field | The text color as a solid fill, with the accent as its label color. The inverse of the page's primary button |
| Lines and pattern | The field shifted 12 to 16 percent toward the text color, 1px |

- One field per view, on the focal object. The page behind it stays neutral.
- Outside the field the accent still appears, kept small: a link, a focus ring, the selected state. Count the places it appears across the whole view. Past four, turn the least important one neutral.
- A tint of the accent, 8 to 10 percent over the surface color, is the quiet form of the same color for selected states and washes. It counts as one of the places.

## Status colors keep their meaning

Success, warning and error stay recognizable. Keep each within about 15 degrees of its expected hue and bring its lightness and chroma in line with the palette, so a red on a dawn background is a warm terracotta red and not a default `#EF4444`. Never let a status color be the accent, and never drop a status the source has.

## Measure text where it actually sits

A gradient has no single contrast value, and a palette that passes on paper can fail once the layout puts a label over the bright band. Measure after the layout exists, at each element's real position: read its top and bottom from the render or the frame, and take the gradient's color at those heights. Measure the secondary and tertiary tones too, since they fail first.

For every text element:

1. Find the lightest and darkest region it can sit over, including while scrolling.
2. Compute the ratio against the worst one.
3. Body text and labels need 4.5:1. Text at 24px and up, or 19px bold, needs 3:1. So do icons and chart marks that carry meaning.

When a pair fails, fix it in this order:

1. **Move the text** to a region where it passes.
2. **Switch the text tone** for that region: dark text on the bright band, light text on the dark base.
3. **Put a surface behind it**: a dark-tinted glass or a solid step.
4. **Change the background** stop's lightness.

White text on a bright warm band is the usual failure. A peach at OKLCH lightness 0.74 gives white about 2.3:1, and laying white-tinted glass over it makes that lower. Dark text on the same peach measures about 7.6:1.

Report each pair you measured with its ratio. A pair you could not measure is **Not verified**.

## Deliver the theme the source has

If the source is dark, the result is dark, or whatever the atmosphere makes it. Do not add a second theme unless asked. If the project has both light and dark, define the atmosphere and the roles for both and measure both.

## Before you finish

| You notice | Fix |
| --- | --- |
| `#6366F1`, `#8B5CF6`, `indigo-*`, `violet-*` or `purple-*` still present, with no brand behind them | Replace with roles sampled from the background |
| `#0F172A`, `#111827`, `slate-900` or `gray-50` as the page color | Build the atmosphere from the brief |
| A gradient, image or blurred shape behind a table, a form or an editor | A quiet tinted neutral |
| Text tones on an accent field made with `opacity` | Solid mixes toward the field, measured against it |
| A filled accent button sitting on an accent field | Invert it: the text color as fill, the accent as label |
| The accent in more than four places in one view | Turn the least important one neutral |
| A wash stronger than 12 percent, or one that runs behind a table, form or body text | Lower it, or stop it before that content |
| Two fields of the accent in one view | Keep the one on the focal object |
| A bleed, a field and a wash together in one view | Keep one |
| A colored header that ends at a hard line above a white page | Fade it into the page and set a surface across the transition |
| A second hue used for the second level of emphasis | The text color as a fill |
| A surface scale with steps of mixed hue, or more than four steps | Two or three steps in the background's hue |
| A background gradient chosen without a line in the brief saying what it stands for | Go back to `unslop-direction` |
| Blurred circles or corner glows behind content | Delete them |
| A two-stop gradient between opposite hues with a gray middle | Add a middle stop or interpolate `in oklch` |
| `#FFFFFF` or `#000000` text or shadows on a colored background | The tinted near-white or near-black |
| A neutral with zero chroma | Tint it with the background hue |
| Sibling icons or stats in unrelated hues | One color, unless the hues encode categories |
| More than one filled accent element in a view | Keep the primary |
| A status color replaced by the accent, or removed | Restore it, tuned to the palette |
| A brand color changed | Restore it and build around it |
| Contrast measured against the stops, before the layout placed the text | Measure again at each element's real position |
| Small secondary text sitting directly on the transition into the bright band | Darken the stop behind it, raise the tone's strength or put it on a surface |
| A contrast claim with no computed ratio | Compute it against the worst region, or mark it **Not verified** |
| White text over the gradient's brightest band | Dark text there, or a dark-tinted surface |
| Text tones made with `opacity` over a gradient | Solid values, so they can be measured |
| A hex literal in a component where the project has color tokens | Add or reuse a role token |
| A light theme added that nobody asked for | Remove it |
