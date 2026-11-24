---
name: unslop-code
description: Applies a restyle to a coded screen without touching its behavior, and rebuilds a screen from a screenshot when there is no source. Covers finding the stack and tokens, restyling through tokens and classes, keeping data bindings, handlers and accessibility intact, adding fonts, and before and after screenshots. Use when unslop or any unslop-* pass works on React, Vue, Svelte, SwiftUI, Flutter, HTML or CSS, or on an image of a UI.
---

# Code adapter

This skill is how the unslop passes change a screen that exists as code, or produce one from an image. It holds no design rules. It holds the mechanics: where the look lives in a codebase, how to change it without changing what the screen does, and how to show the difference.

What to change is decided by `unslop-layout`, `unslop-surfaces`, `unslop-dataviz`, `unslop-typography`, `unslop-color` and `unslop-navigation`. The content contract and the pipeline belong to `unslop`. Figma sources belong to `unslop-figma`.

## Restyle the view, leave the behavior

A reskin's diff is presentation: styles, class names, tokens, markup structure where the layout changed, an SVG where a chart changed form. It is never data fetching, state, routing, validation or business logic. If a design change seems to need one of those, it is a proposal for the report, not an edit.

Write every change in the project's own idiom: its styling system, its component library, its token names. Never introduce a second styling approach. Never add a dependency without saying so and getting a yes, with one stated exception for fonts below.

## 1. Find where the look lives

Before changing anything, establish:

- **The stack.** Framework, styling system (Tailwind and its version, CSS modules, styled components, a native UI toolkit), component library, icon set, chart library.
- **The tokens.** A Tailwind theme, CSS custom properties, a theme object, a design-system package. Which colors, radii, spacing steps, fonts and shadows already exist.
- **The files that render this screen.** The route or screen component and the components it uses. Note which components are shared with other screens.
- **How to see it.** A dev server command, a Storybook, a simulator, a preview. Take a screenshot of the screen as it is now, at the width it is designed for. That is the "before".
- **What the project says about itself.** `AGENTS.md`, `CLAUDE.md`, a design-system doc, lint rules for styles.

Work on a branch. If the working tree has uncommitted changes that are not yours, leave them alone and say so.

## 2. Write the contract from the code

For each element, record where its content comes from: a prop, a query field, a store value, a translation key, a literal. Record every handler and link with its target. Record the states the code branches on: loading, empty, error, selected.

A string that comes from a translation file is changed in that file, in every locale the file has, or not at all. A `relabel` that updates one locale and leaves the others is a bug.

## 3. Change tokens before components

Most of a restyle belongs in the token layer:

| Change | Where it goes |
| --- | --- |
| Palette roles, atmosphere stops | Semantic color tokens |
| Typeface, type scale | Font and text tokens |
| Radius family | Radius tokens |
| Spacing scale | Spacing tokens, only if the project has none |
| Glass, shadows | Shared utilities or surface tokens |

If the screen's tokens are shared with the rest of the app, changing them restyles the whole app. Decide which is wanted:

- **The request is this screen only.** Scope the new values: a theme class or data attribute on the screen's root that redefines the semantic tokens beneath it. The rest of the app is untouched.
- **The request is the product.** Change the tokens at the root and check the other screens that consume them.

Say in the report which one you did. Never restyle a shared component for one screen's sake. Wrap or scope it.

## 4. Edit components without breaking them

Keep, exactly as they are:

- Data bindings, props, hooks, queries, state and effects.
- Event handlers and their targets, links and routes.
- `id`, `data-testid`, `name` and other attributes tests and analytics hook onto.
- Accessible names, roles, labels, `alt` text and focus behavior. When a visible label is shortened, the accessible name keeps the full meaning.
- Conditional branches for loading, empty and error. Restyle each branch. Do not delete one.
- Semantic elements. A `<button>` stays a `<button>`.
- Translation calls. A string wrapped in a translation function stays wrapped.

Change freely:

- Class names, style objects and CSS for the screen.
- The wrapper structure, where layout changed: fewer nested containers is usually the result.
- The order of sections, in `full` mode, keeping DOM order equal to visual order.
- A chart's rendering, when its form changes: a new SVG fed by the same data props.

Remove what the passes removed: the icon tile wrapper, the border classes, the glow, the blob elements. Deleted code is the goal of several passes. Dead styles and unused imports left behind are not.

In `full` mode, a `cut` or `demote` of an element with a data binding or handler follows the contract: proposed unless the user asked for a rework or approves.

## 5. Fonts

A new typeface is the one new asset a restyle normally needs. Add it the way the project already loads fonts:

- A framework font loader, such as `next/font`, when the project uses one.
- A self-hosted file or package, when fonts are self-hosted.
- A stylesheet link, when the project already loads fonts that way.

Load only the weights used, keep a fallback stack and set `font-display: swap` or the loader's equivalent. Name the addition in the report. If the project has no way to add a font, or the user said no new assets, keep the existing family and apply the weight and scale rules only.

## 6. Check it still works

- Run the project's typecheck, lint and tests. A restyle that fails a snapshot test has changed a snapshot: update it only when the change is the intended visual one, and say so.
- Render the screen and take the "after" screenshot at the same width as the "before".
- Render each state the code has: loading, empty, error.
- Check the narrowest supported width, 320px for web, and a long-string case for every text slot that takes data.

A check you cannot run is reported as **Not verified**. Do not claim the screen looks right from the diff.

## From a screenshot

When the source is an image and there is no code or Figma file:

1. **Transcribe everything first.** Every string, number, unit and label, into the content contract, before designing. Mark any character you cannot read with certainty and ask, or flag it. Do not guess a digit.
2. **State the scale.** Sizes read from an image are estimates. Say what width you assumed, such as 390 for a phone capture.
3. **Build the result, not the source.** Do not recreate the original first. Go from the contract and the brief straight to the restyled screen.
4. **Deliver one self-contained file** unless a stack was requested: a single HTML file with inline CSS, real text, inline SVG for the hero, system-safe font loading. No build step, no external images. Size it to the source's dimensions and center it on a neutral page.
5. **Mark sample data as sample.** The values are the screenshot's. Name them as props or constants at the top so they can be wired later.
6. **Crop the images, never redraw them.** A logo, an avatar, a photo or a product shot is content. Crop it from the screenshot, embed it in the file, and report it as a low-resolution stand-in to be replaced with the real asset. Do not retype a logo in a similar font or generate a replacement image.

The same approach applies when Figma can be read and not written.

## Before you finish

| You notice | Fix |
| --- | --- |
| A change to a fetch, a query, a reducer, a route or a validator in the diff | Revert it and list the need as a proposal |
| A handler, `data-testid`, `id` or `aria-*` attribute gone from the diff's removed lines | Restore it on the restyled element |
| A loading, empty or error branch deleted | Restore it and restyle it |
| A hardcoded string where the source used a prop, a variable or a translation key | Restore the binding |
| A number in the markup that the source computed from data | Restore the computation |
| A `<div onClick>` where the source had a `<button>` or a link | Restore the element |
| A new package in the manifest that was not approved | Remove it and use what the project has, or ask |
| Raw hex, arbitrary pixel values or inline styles in a project that has tokens | Map them to tokens, adding role tokens where needed |
| Root tokens changed when the request was for one screen | Scope the values to the screen |
| A shared component restyled for this screen's sake | Revert it and scope or wrap instead |
| A label changed in one locale file only | Change every locale or none |
| Unused classes, imports or wrapper elements left from the old design | Remove them |
| "Looks good" reported with no after screenshot | Render it, or mark it **Not verified** |
| A digit or word in the result that was unclear in the screenshot | Flag it. Do not ship a guess as data |
