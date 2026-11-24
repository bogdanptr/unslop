# Font pairings

Starting pairings by direction, what to check before using one, and how the choice is expressed in Figma and in CSS. All families here are open-licensed. Availability and shipped weights change, so confirm both before committing.

## Before choosing

1. **Is it available where the result lives?** In Figma, the family must be installed or be a Google font. In code, check how the project loads fonts and whether it can add one. Adding a font file or dependency follows `unslop-code`.
2. **Does it ship the weights?** A hero at 300 needs a real 300. Several good display faces ship one weight only.
3. **Does it cover the content?** Check the contract for accented Latin, Cyrillic, Greek, Arabic, CJK. A face without the glyphs falls back mid-word.
4. **Does it have tabular figures?** Needed for timers, prices and columns. Most of the sans families below do.

## By direction

| Direction | Display and figures | Interface text | Notes |
| --- | --- | --- | --- |
| Atmospheric | Manrope 300 | Manrope 400 to 500 | One family. Open, calm numerals |
| Atmospheric | Outfit 300 | Outfit 400 | Rounder, friendlier |
| Atmospheric | Urbanist 300 | Urbanist 400 to 500 | Narrower, elegant at large sizes |
| Instrument | Geist 400 | Geist 400, Geist Mono for figures | Tight and exact |
| Instrument | IBM Plex Sans 400 | IBM Plex Sans, IBM Plex Mono for figures | More character, slightly technical |
| Editorial | Instrument Serif 400 | A neutral sans such as DM Sans | The serif ships regular only. Use it large |
| Editorial | Fraunces 300 to 400 | Figtree 400 | Warm, with a real light weight |
| Editorial | Newsreader 400 | Hanken Grotesk 400 | For reading-heavy screens |
| Tactile | Figtree 400 to 500 | Figtree 400 | Soft without being childish |
| Tactile | Plus Jakarta Sans 400 | Plus Jakarta Sans 400 to 500 | Wider, generous |
| Mono utility | Hanken Grotesk 400 | Hanken Grotesk 400 to 500 | Neutral with good rhythm |
| Mono utility | Onest 400 | Onest 400 to 500 | Slightly warmer, wide script coverage |
| Content-led | DM Sans 400 | DM Sans 400 to 500 | Stays out of the content's way |
| Graphic | Bricolage Grotesque 700 to 800 | DM Sans 400 | The one direction with a heavy display line |
| Graphic | Unbounded 600 | Figtree 400 | Very wide. One short line only |

A single family at two or three weights is the safer choice. Use a pairing when the brief's voice asks for contrast between display and interface.

## Faces to treat as defaults

Inter, Roboto, Poppins, Open Sans, Montserrat, Space Grotesk and the system stack. None is bad. Each is so common on generated screens that choosing it is the same as not choosing. Keep one only when the brand documents it.

## In CSS

```css
:root {
  --font-display: "Manrope", ui-sans-serif, system-ui, sans-serif;
  --font-text: "Manrope", ui-sans-serif, system-ui, sans-serif;
}

.hero-value {
  font-family: var(--font-display);
  font-size: 4rem;
  font-weight: 300;
  line-height: 1;
  letter-spacing: -0.02em;
  font-variant-numeric: tabular-nums;
}

.hero-unit {
  font-size: 0.55em;      /* relative to the value */
  font-weight: 400;
  color: var(--color-text-tertiary);
}

.overline {
  font-size: 0.6875rem;
  font-weight: 500;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: var(--color-text-secondary);
}
```

Always keep a fallback stack. Load only the weights the screen uses.

## In Figma

- Letter spacing is a percentage: -2 percent for the hero, 7 percent for an uppercase overline.
- Line height as a percentage: 100 for the hero figure, 140 for body.
- Set case with the text layer's case setting, so the characters stay as written.
- Turn on tabular figures in the type details panel for changing values.
- A text layer can carry mixed styles, so the value and unit in `7h 42m` can stay one layer with two sizes. Keep it one layer when you can. The string then remains intact for checking.
- Before changing characters or style through the Plugin API, the font must be loaded for that layer, including every font in a mixed-style layer.
- Where the file has text styles, restyle through them or create a small set of new ones named by role. Do not leave every layer with local overrides.
