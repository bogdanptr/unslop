---
name: unslop-surfaces
description: Cleans up cards, panels, borders, icons, radius, shadows, buttons, inputs and overlays on any interface, and applies the chosen material - flat, matte, paper or glass - as the final step. Removes strokes and tinted icon tiles, settles on one radius family and one way of separating surfaces. Use when a screen has too many boxes, bordered cards, icons in colored squares, glowing buttons, default-looking inputs or inconsistent corners, or as the surfaces and finish passes of unslop.
---

# Surfaces

This skill decides what each container is made of and removes the ones that are not needed. It runs twice in the pipeline: early, to strip borders, tiles and glows down to plain structure, and last, to apply the material the direction brief chose.

Which sections exist and how they are spaced belongs to `unslop-layout`. Colors of fills and text belong to `unslop-color`. Chart marks and table rules belong to `unslop-dataviz`. Navigation structure belongs to `unslop-navigation`.

## Subtract first, exact values after

Most of this pass is removal, and removal needs no taste: a border that does no work goes. Do that part completely.

The values that remain are exact. One padding, one radius family, one separation method, the stroke widths and the material recipe below. A card at radius 16 beside one at 14 is a defect.

Where the project has radius, shadow or surface tokens, or a component library, use them and fix only what is inconsistent with them. Restyle a library through its theme, not by overriding each component.

## A box has to earn its edge

A container needs a reason: it groups several things that would otherwise read as separate, or it is a control that needs a shape. A single value with its label does not need a box. Neither does the view's focal point, a page section on a marketing page, or a form that is the only thing on its page.

For the containers that stay, separate them from the background **one way**:

| Method | Use it when | Value |
| --- | --- | --- |
| Space alone | The group is obvious from proximity | No fill, no stroke |
| A fill step | The background is flat | Dark: surface 4 to 6 percent lighter than the page in OKLCH lightness. Light: white, or the raised step, on a page whose lightness `unslop-color` sets |
| A translucent fill | The background is a gradient or image | See **The material goes on last** |
| A hairline | Rows in a list or a table, or a flat direction that uses rules | 1px at 8 to 12 percent of the text color |

Never a stroke plus a contrasting fill plus a shadow on the same element. That triple is the default card. Pick the one the brief's material calls for and delete the others.

Never a bordered card inside a bordered card. The inner one loses its edge and keeps only padding, or the outer one goes.

## One corner language

Before any value, choose how corners behave across the whole view. There are three languages, and a view speaks one:

| Language | Corners | Suits |
| --- | --- | --- |
| Round | Pills and circles. Containers take a large radius, controls are fully round | Playful, consumer, soft directions |
| Soft | Rounded rectangles everywhere, on one radius family. Nothing is a pill or a circle | Most product interfaces. Reads as precise and calm |
| Square | 0 to 4 everywhere | Instrument, editorial, dense work views |

Fully round is a language, not an exemption. A pill-shaped search bar above a rounded-rectangle navigation bar, or circular icon buttons beside rounded-square tiles, is two languages in one view, and it is the most common way a careful restyle still looks unsettled.

- In the soft and square languages, buttons, chips, icon buttons, avatars, selected-state capsules and bars all take the family's radii. No `999px`, no `50%`.
- In the round language, containers too large to be pills take the largest radius of the family, and every control inside them is a pill or a circle.
- Shapes that are round because of what they are stay round in any language: a status dot, a radio button, a spinner, a chart mark, a notch cut into an edge.

## One radius family

Pick one base radius for cards from the brief's material, then derive the rest:

| Element | Radius |
| --- | --- |
| Cards, panels and tiles | One value. 12 to 16 is a calm default, 20 to 28 for soft or glass directions on a phone, 6 to 10 for instrument, paper and dense work views |
| An element nested inside a padded container | The container's radius minus the padding, minimum 4. A 24 bar with 8 padding holds 16 inner corners. Choose the padding so the result is a value you already use |
| Chips, tags, segmented controls | The nested value in the soft language, fully round in the round language. One choice for all of them |
| Buttons, icon buttons, inputs, avatars | One value for all, so a field and the button beside it match. The inner value in the soft language, fully round in the round language, 6 to 10 on work views |
| Dialogs, sheets, popovers, floating bars | The card radius or one step larger, never smaller |
| Images and media | The radius of the surface they sit in, following the nesting rule |

Two values are usually enough: one for containers, one for what sits inside them. More than three distinct radius values on one screen means the family has drifted. The device frame is not counted.

Big radii belong to big, soft, sparse surfaces. On a dense table or a toolbar, 24 on every corner wastes space and reads as a toy.

## Take icons out of their boxes

An icon in a tinted rounded square, one hue per metric, is the most recognizable detail of a generated screen. Remove the tile and keep the icon:

- The icon sits inline with its label, on the same baseline, 4 to 8 apart.
- Size is 1 to 1.25 times the label's font size. Beside a 13px label, a 14 or 16 icon.
- Stroke is 1.5px beside regular text, 2px beside medium or semibold.
- **Every icon is a real file from one published set.** Never draw an icon from memory. Use the project's set when it has one, otherwise choose one open-source set, fetch each icon's SVG and place it inline with `currentColor`. Which sets, their licences, the package names and the file addresses are in [icons.md](icons.md).
- Color is the label's color, or the single accent when the icon marks something active. Not one hue per item.
- Where the label already says it, consider whether the icon is needed. An icon that repeats its label is decoration.

A leading mark on a list row is a different thing. Where rows are scanned by their first element, such as bills, files, contacts or transactions, each row may open with a small mark in a container: all containers the same size, shape and neutral fill, all icons the same single color. What makes the tile a tell is one hue per item and a tile on every label. One neutral style on rows that are scanned is a list.

Never swap an icon for a different meaning. A bell stays a bell.

## Controls of one kind share one treatment

The rule above is for icons that label something. An icon that is itself a button is a control, and controls of one kind look alike across the view.

- Pick one treatment for icon buttons and use it everywhere in the view: a filled circle or rounded square on the surface or control color, or bare. If any icon button in the view has a container, every icon button in the same row has one, at the same size.
- Take the shape, size and fill from controls the view already has. A new control borrows from the family, it does not start a second one.
- Things that sit beside controls and act like them, such as an avatar that opens the account, take the same outer size and a matching edge.
- Bare icon buttons are for dense toolbars and table rows, where every one of them is bare.

## A focal surface can carry the subject's pattern

Where `unslop-direction` names a full-strength object, its surface can carry a pattern taken from what the product is about. This is the one place decoration is added, and it has to belong to the subject.

| Subject | Pattern |
| --- | --- |
| Money, documents of value | Engraved line work, as on a banknote or a certificate |
| Terrain, travel, routes | Contour lines or a faint map grid |
| Instruments, measurement | A ruled grid or tick marks |
| Sound, signal | A waveform or concentric rings |
| Time, cycles | Arcs or orbit lines |
| Paper, records | A ruled or dotted sheet, a perforated or torn edge |

- Lines are 1px, in the surface color shifted 12 to 16 percent toward the text color. The pattern is visible on a second look, not the first.
- One pattern, on one surface. Regular and geometric, never a random scribble or a blurred blob.
- Keep its densest part away from small text. Body-size text sits over the plain area or the sparse edge of the pattern.
- It is decoration and marked as such: hidden from assistive technology, and never shaped like a chart or a scale.
- Draw it as vector lines inside the surface, clipped to its radius.

## Shadows are soft, tinted and rare

- A shadow is for an element that floats over other content: a sheet, a menu, a floating button, a floating bar. A card resting on the page does not need one. The one exception is the surface that holds the view's focal region: on a light page where the fill step alone is faint, it may take the soft two-layer shadow at the low end of its range. No other resting surface does.
- Build it from two layers at low opacity, such as `0 1px 2px` at 6 percent and `0 8px 24px` at 8 percent, in a dark tone of the background's hue. Never pure black on a colored background.
- No colored glow under buttons. Delete any shadow in the accent color with a blur above 12.
- On dark flat backgrounds shadows do nothing. Use a fill step.

## Buttons are solid

- The primary button is a solid fill of the accent with the on-accent text color. Remove gradients from buttons. On an accent field the fill and label swap, following `unslop-color`.
- One filled button per view. Secondary actions are a quiet fill at the surface color or a hairline outline, and tertiary ones are plain text. Three levels at most.
- One height per level of density: 44 to 52 on a phone, 32 to 40 on desktop. A button and the input beside it are the same height.
- A circular or pill primary button is a good fit when the label is one short word. Minimum touch target 44 by 44 on touch screens.
- Hover, pressed, focused and disabled are steps of the same color, not new colors. Keep every state the source has.
- Keep the label and the handler. Rewording belongs to `unslop-navigation`.

## Inputs look like one family

Generated forms use the component library's defaults untouched: a gray-bordered box with a blue focus ring.

- One field style for text inputs, selects, date pickers and textareas: the same height, radius, padding and edge.
- The edge is a hairline at 12 to 20 percent of the text color, or a fill step with no stroke. A field needs a visible boundary: 3:1 against the surface for the edge or the fill.
- The label sits above the field, at label size in the secondary or primary tone. Placeholder text is never the only label.
- Focus is a 2px ring or a stronger edge in the accent, clearly visible. Never remove a focus indicator.
- Checkboxes, radios and switches take the accent when on and the field's edge when off. One size for all of them.
- Errors are text under the field in the error color with the edge in the same color. Not a red fill across the field.
- Group fields with space and a plain section heading. A card around every group of three fields is a tell.

## Rows are separated lightly

- A list row is separated by space or one hairline, not by a card per row.
- Hover and selected states are one quiet fill step, shared with tables and menus.
- A row that navigates shows it once, with a chevron or by its whole surface responding. Not both and a button.

## Floating bars are separate objects

A control that stays fixed while content scrolls, such as a navigation bar, a search or assistant field, or a toolbar of actions, can float over the page instead of being docked to an edge.

- Inset 12 to 16 from the screen edges, with the card radius or larger, and the soft two-layer shadow.
- Content scrolls beneath and fades out behind the bars: a gradient from the page color to transparent over the 32 to 48 above the top bar. No hairline, no opaque strip.
- **Two floating bars must not read as one.** Leave 8 to 12 between them and make them differ in tone: one on the surface color, the other on the text color with light text. Two bars of the same fill stacked together merge into a single block.
- The darker, heavier bar goes to the control the product wants used most. Navigation is the quieter of the two.
- Each bar holds one kind of thing. A search or assistant field is not navigation and does not share a container with it. Controls that belong to the field, such as a voice button, sit inside its bar.

## Overlays float, and only overlays

- A dialog, sheet, menu or popover is the one kind of surface that takes a shadow and sits above a dimmed or blurred page.
- One scrim: the background's darkest tone at 40 to 60 percent. Not pure black.
- A dialog is 400 to 560 wide on desktop and holds one decision. Its radius is the card radius or one step larger.
- No card inside a dialog. The dialog is the card.

## The material goes on last

Run this step after `unslop-color` has built the background. It applies the material the brief chose to the surfaces that survived, the same way everywhere:

| Material | Surfaces are | Use when |
| --- | --- | --- |
| Flat | Fill steps and no shadows. Hairlines where rows need them | Work views, tools, most product interfaces |
| Paper | No cards where rules and space will do. One page tone, hairline rules, ink-like text | Documents, records, reading, editorial |
| Matte | A fill step with the soft two-layer shadow, larger radii | Consumer products with a warm, physical feel |
| Glass | A translucent blurred fill with a hairline | Only over a gradient or image atmosphere |

Most interfaces are flat or paper. Glass is the exception: it needs something behind it, and over a flat fill it is a gray rectangle with a performance cost. Never put glass on a work view, a form or a table.

The glass recipe, for surfaces over a gradient or image:

```css
.glass {
  background: rgb(255 255 255 / 0.10);          /* 0.08 to 0.14 */
  backdrop-filter: blur(24px) saturate(160%);   /* blur 20 to 30 */
  -webkit-backdrop-filter: blur(24px) saturate(160%);
  border: 1px solid rgb(255 255 255 / 0.12);    /* hairline, 0.10 to 0.16 */
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / 0.22),      /* top highlight */
    0 8px 32px rgb(0 0 0 / 0.12);               /* soft lift */
}
```

- **One level.** No glass on glass. Chips inside a glass card are a slightly stronger fill with no blur of their own.
- **Few surfaces.** A group of tiles, a navigation bar, a sheet. Not every element.
- **One treatment.** Every glass surface on the screen gets the same fill, hairline and highlight. A drop shadow on one and none on the others reads as two materials.
- **Light glass lowers contrast for white text.** Over a bright region of the background, white text on white-tinted glass gets worse, not better. Use a dark-tinted glass there, in a dark tone of the background hue, or dark text. Around 0.25 opacity is enough for large text. Small text over a bright band needs 0.40 to 0.50. Measuring it belongs to `unslop-color`.
- **The hairline is part of the material**, so it is the one border this skill adds. It is white at low opacity, never gray.
- **Give it a fallback.** Without `backdrop-filter`, use a solid surface color at 85 to 90 percent opacity.

The Figma version and the light-background variant are in [glass.md](glass.md).

## Before you finish

| You notice | Fix |
| --- | --- |
| A stroke, a contrasting fill and a shadow on one card | Keep the one the material calls for |
| `border` with `border-gray-*`, `border-white/10` or a Figma stroke on every card | Remove the strokes. Separate by fill step or space |
| A bordered or filled frame directly inside another | Strip the inner one to padding only |
| An icon wrapped in a tinted square or circle | Remove the wrapper, set the icon inline with its label |
| A bare icon button beside icon buttons that have a container, or an avatar at a different size from the buttons beside it | One treatment and one size for the row |
| Sibling icons in different hues with no meaning behind the hues | One color, the label's |
| An icon whose path was written by hand, or icons with uneven stroke and corner styles | Replace each with the real file from the chosen set |
| Icons from two sets in one view | One set |
| An icon loaded from a CDN link in the result | Inline the SVG |
| More than three radius values on the screen | Reduce to the family |
| `rounded-full`, `999px` or `50%` on controls in a view whose containers are rounded rectangles, or the reverse | One corner language for the view |
| A circular avatar or icon button beside rounded-square controls | The family's inner radius |
| A nested element with the same radius as its padded parent | Parent radius minus padding |
| `shadow-*-500/50` or any accent-colored shadow | Delete it |
| `#000` shadow on a tinted or gradient background | A dark tone of the background hue at lower opacity |
| A gradient fill on a button | Solid accent |
| More than one filled button in a view | Keep the primary, make the rest quiet |
| A button and the input beside it at different heights or radii | One height, one radius |
| Inputs with the component library's default gray border and blue ring | The field style above, with the accent for focus |
| `outline: none` or a removed focus ring with nothing in its place | Restore a visible focus indicator |
| A card around each small group of form fields | Space and a section heading |
| A card per list row | Rows separated by space or a hairline |
| A shadow on a card that rests on the page | Remove it. Shadows are for overlays and floating controls |
| Two fixed bars of the same fill touching or stacked | Separate them by 8 to 12 and give them different tones |
| A search or assistant field inside the navigation's container | Its own bar |
| A hairline or opaque strip where content meets a floating bar | A fade from the page color |
| A pattern on a surface that is not the focal object, or on more than one surface | Remove it |
| A pattern with no link to the subject, or one that is random or blurred | The subject's own pattern, regular, in 1px lines |
| Small text over the dense part of a pattern | Move the text or thin the pattern there |
| Glass on a work view, a form or a table | Flat or paper |
| Radius of 20 or more on dense rows, toolbars or table cells | 6 to 10 |
| `backdrop-filter` over a flat single-color background | Remove the blur and use a fill step |
| A glass surface inside a glass surface | Remove blur from the inner one |
| A material applied before the background exists | Undo it and run this step after `unslop-color` |
| White text on light glass over a bright background region | Dark glass or dark text, then measure |
