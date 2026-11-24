---
name: unslop-figma
description: Reads a Figma frame for restyling and writes the restyled version back as a copy beside the original. Covers reading values and text through a Figma MCP server, duplicating frames, editing with auto layout and variables, and what to do with no write access. Use when unslop or any unslop-* pass works on a Figma link, file or selection.
---

# Figma adapter

This skill is how the unslop passes get a screen out of Figma and put the restyled one back. It holds no design rules. It holds the mechanics: what to read, where to write and how to leave the file in a state a designer can keep working in.

What to change is decided by `unslop-layout`, `unslop-surfaces`, `unslop-dataviz`, `unslop-typography`, `unslop-color` and `unslop-navigation`. The content contract and the pipeline belong to `unslop`. Code sources belong to `unslop-code`.

## The original is never edited

Every change goes on a duplicate. The source frame stays exactly as it was, so the before and after sit side by side and nothing is lost if the result is rejected. This is a hard rule, not a preference.

Tool names below are the official Figma MCP server's. Other Figma servers expose the same capabilities under other names, so search the available and deferred tools for `figma` before concluding there is no access. Where the server ships its own skill for calling its tools, load that first and follow its calling rules. A server that offers only an authenticate tool is connected and signed out: ask the user to sign in.

## 1. Find the frames

A Figma URL carries the file key after `/design/` or `/file/` and the node in `node-id`, written `12-34` in the URL and `12:34` to the tools. On a branch URL, use the branch key as the file key.

A link with no `node-id`, or to a whole page, names no frame. List the top-level frames with `get_metadata` and confirm which ones are in scope before reading any of them. Frames showing the same screen at different widths are one screen.

## 2. Read everything the contract needs

| Call | Gives you | Use it for |
| --- | --- | --- |
| `get_screenshot` | A render of the node | The "before", the squint and swap tests, the comparison target |
| `get_design_context` | Structure, exact values, text, variables in use, component instances | The content contract and the diagnosis |
| `get_metadata` | The layer tree with ids, names and sizes | Large frames, finding which children to read |
| `get_variable_defs` | Variables and their values | What the file already has for color, spacing and radius |

Take the text from the layer data, never by reading the screenshot. A screenshot misreads `1h 48m` as `1h 46m`.

Check what the file documents before judging it: variable collections, color and text styles, a cover or guidelines page. A style named for a brand is a fixed decision.

This step is done when you hold a screenshot of each frame, every text string with its layer id, the component instances and the variables in use.

## 3. Duplicate, then work on the copy

1. Clone the source frame.
2. Place the clone on the same page, to the right of the source with a gap of 100 or more, clear of other frames. Check the neighbours' positions first so nothing overlaps.
3. Name it `<original name> / unslopped`.
4. Record both node ids. Every later write targets the clone or its children.

For several screens, lay the copies out in a row under or beside their originals in the same order.

With the official server, writes go through `use_figma`, which runs Plugin API code in the file. Keep each call to one pass or one logical change, and take a screenshot of the clone after it.

## 4. Edit in ways a designer can keep using

- **Keep text as text.** Change a text layer's style, not its characters. Never outline, flatten or rasterize text. When the Plugin API changes a text layer, load every font the layer uses first, or the call fails.
- **Split styling, not layers, where possible.** `7h 42m` with a smaller unit can stay one text layer with mixed sizes. That keeps the string intact for the contract check.
- **Move layers, do not retype them.** When the structure changes, build the new frames and move the existing text layers into them. A moved layer keeps its id and its characters, so the contract check stays a comparison of ids. Create a new text layer only for a marked placeholder.
- **Use auto layout.** Express spacing as gap and padding on auto layout frames, on the spacing scale. Do not position by absolute x and y inside a layout. The one exception is an element that deliberately overlaps a group, such as an action at the center of four tiles: make it a child of the group with absolute positioning and center constraints, so it follows the group when the group resizes.
- **Bind to variables and styles.** If the file has color or spacing variables, bind to them and add the new roles as variables in a collection named for the restyle. If it has none, create a small set: the color roles, the radius, the spacing steps. Leave no raw hex on text.
- **Respect components.** Restyle an instance through its properties or overrides. Change a main component only when it lives in this file and the change is meant for every use. Never detach an instance to edit it. If the design cannot be reached through the component, build that piece from plain frames in the copy and note it.
- **Name what you make.** `Hero / arc`, `Metric / deep sleep`, not `Frame 427`. A layer that encodes a value carries the value in its name. An imported SVG arrives with children named `Vector`: name those too.
- **Delete what is cut.** Removed elements are deleted from the copy, not hidden. The ledger and the untouched original are the record.
- **Keep images.** Reuse the source's image fills. Do not replace or regenerate them.

Recipes for specific effects are with their owners: the glass effect in `unslop-surfaces`, gradient fills and grain in `unslop-color`, arcs and proportional marks in `unslop-dataviz`, type settings in `unslop-typography`.

## Recipes written for CSS need converting

The recipes in the pass skills give CSS values. Three of them change in Figma:

| Recipe says | In Figma |
| --- | --- |
| `backdrop-filter: blur(24px)` | A background blur effect with radius 48. Figma's blur radius is twice the CSS value |
| A gradient with `oklch()` stops | Convert each stop to hex and keep the positions. Figma interpolates between stops in sRGB, so the bands between stops differ from the CSS render |
| A text color with alpha, such as secondary text at 84% | One color variable whose value carries the alpha, bound to the text fill |

Because the gradient renders differently, contrast measured on an HTML version does not carry over. Measure again on the copy: for each text layer, interpolate the gradient stops in sRGB at the layer's top and bottom edge, composite the surface fill over that if the layer sits on glass, and compute the ratio against the text color. The thresholds are in `unslop-color`.

## 5. Look after every pass

Take a screenshot of the copy after each pass and look at it before starting the next. A write that succeeded is not a write that looks right: text overflows, a blur renders as a solid, a clone clips its children. Fix what the render shows before moving on.

At the end, take the final screenshot of the copy at the same scale as the source's.

## With no write access

When the server can read and cannot write, or there is no Figma tool at all:

1. Say so in one line. Do not stop.
2. Build the result as a self-contained HTML file at the frame's size, following `unslop-code`, **From a screenshot**, using the values read from Figma.
3. Report where the file is and that it is a rendering of the direction, not a Figma frame.

With no Figma access at all and only a pasted screenshot, the source is a screenshot. Follow `unslop-code`.

## Before you finish

| You notice | Fix |
| --- | --- |
| "Figma is not connected" said before any tool search | Search the tools for `figma` first |
| A write that targeted the source frame's id | Undo it and redo it on the clone |
| The clone placed on top of another frame | Move it to clear space |
| Text in the contract that was read from the screenshot | Read it from the layer data |
| A text layer whose characters changed, apart from a recorded `relabel` | Restore the characters from the contract |
| Text outlined or flattened to a vector | Restore it as a text layer |
| An instance detached from its component | Reattach and use overrides, or note why it could not be done |
| Children positioned absolutely inside an auto layout frame | Use gap and padding |
| Raw hex fills where variables exist or were created | Bind them |
| Layers named `Frame 12`, `Group 3`, `Rectangle 9`, `Vector` in the copy | Name them by role |
| A text layer in the copy whose id is not a clone of a source layer, and that is not a placeholder | Move the original layer in and delete the retyped one |
| A background blur radius copied straight from a CSS recipe | Double it |
| Contrast figures taken from an HTML render of the same design | Measure on the Figma copy |
| Cut elements left as hidden layers | Delete them |
| A pass finished with no screenshot of the copy looked at | Take one and look |
