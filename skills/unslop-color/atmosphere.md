# Atmosphere recipes

Backgrounds with their stops, a worked palette derived from one, the contrast formula and how to build each in CSS and Figma. Values are OKLCH with the sRGB hex beside them. Treat them as starting points and shift them toward the product.

## Phenomena

Stops run top to bottom.

| Atmosphere | Stops | Stands for |
| --- | --- | --- |
| Dawn | `oklch(0.66 0.10 285)` `#8C89CD` at 0%, `oklch(0.78 0.08 40)` `#E5A691` at 42%, `oklch(0.74 0.13 60)` `#E6964F` at 62%, `oklch(0.30 0.05 50)` `#422616` at 100% | Waking, starting, morning summaries |
| Dusk | `oklch(0.30 0.09 280)` `#262659` at 0%, `oklch(0.50 0.14 340)` `#953D7C` at 55%, `oklch(0.74 0.13 50)` `#EC915C` at 100% | Winding down, evening, endings |
| Night | `oklch(0.16 0.03 265)` `#070D1A` at 0%, `oklch(0.24 0.06 275)` `#171C3B` at 60%, `oklch(0.32 0.08 290)` `#332A58` at 100% | Rest, focus, quiet |
| Deep water | `oklch(0.20 0.05 235)` `#001929` at 0%, `oklch(0.36 0.06 215)` `#084551` at 60%, `oklch(0.54 0.09 195)` `#0B7F7F` at 100% | Calm, depth, breathing |
| Forest | `oklch(0.20 0.03 160)` `#091A11` at 0%, `oklch(0.33 0.06 150)` `#1C3E24` at 55%, `oklch(0.50 0.08 135)` `#4F6D3E` at 100% | Outdoors, growth, slow habits |
| Ember | `oklch(0.18 0.02 30)` `#1A0E0C` at 0%, `oklch(0.30 0.07 35)` `#4B1F14` at 55%, `oklch(0.55 0.15 45)` `#B64E10` at 100% | Energy, training, heat |

Near-white text passes 4.5:1 on every stop of Night, Deep water, Forest and Ember. On Dawn and Dusk it fails on the bright stops, so those two need the per-region text rule in the worked example below.

## Materials and neutrals

| Atmosphere | Page | Surface | Text | Accent example |
| --- | --- | --- | --- | --- |
| Paper | `oklch(0.975 0.008 85)` `#F9F6F1` | `oklch(0.995 0.004 85)` `#FFFDFA` | `oklch(0.22 0.01 60)` `#1E1A16`, secondary `oklch(0.52 0.01 60)` `#6D6863` | `oklch(0.55 0.16 35)` `#BC4527` |
| Studio | `oklch(0.965 0.003 250)` `#F2F4F5` | White | `oklch(0.20 0.005 250)` `#141618` | One saturated color from the brand or the content |
| Ink | `oklch(0.16 0.01 60)` | `oklch(0.21 0.01 60)` | `oklch(0.96 0.01 80)` | A warm light tone, `oklch(0.82 0.10 85)` |

On Paper, the text measures 16.1:1, the secondary text 5.1:1 and the accent 4.9:1 against the page.

Add a light grain to Paper and Ink. Keep Studio clean.

## Worked example: a palette from Dawn

The background is the Dawn gradient. Everything else is taken from it.

| Role | Value | Taken from |
| --- | --- | --- |
| `text-on-dark` | `oklch(0.98 0.01 80)` `#FCF8F1` | Near-white tinted toward the warm stops |
| `text-on-light` | `oklch(0.22 0.035 50)` `#28160B` | The base stop, darkened |
| `accent` | `oklch(0.80 0.14 70)` `#F7AC4D` | The sunrise stop, with lightness and chroma raised |
| `on-accent` | `text-on-light` | Measures 9.1:1 on the accent. Near-white measures 1.8:1 |
| `surface` | Dark-tinted glass, `rgb(40 22 12 / 0.45)` | The base stop as a translucent layer |
| `hairline` | `rgb(255 255 255 / 0.12)` | |

Measured against each region:

| Text | On the top stop `#8C89CD` | On the sunrise stop `#E6964F` | On the base stop `#422616` |
| --- | --- | --- | --- |
| `text-on-dark` | 3.0:1, large text only | 2.3:1, fails | 13.1:1 |
| `text-on-light` | 5.5:1 | 7.3:1 | 1.3:1, fails |

What follows from the numbers:

- The hero sits in the upper half. A 64px figure in `text-on-dark` passes there as large text, and `text-on-light` passes at any size.
- Small text over the sunrise band is `text-on-light`. Its secondary tone at 68 percent drops to about 2.4:1 there, so small secondary text does not sit directly on the bright band.
- Controls and small labels sit on the dark base in `text-on-dark`, or on a dark glass surface, where near-white reaches about 5.3:1 even over the bright band.
- The primary button is the accent with dark text on it.

Run the same table for any gradient before placing text, then measure again once the layout exists.

A common failure with this recipe is small secondary text landing on the transition into the bright band, where it measures under 3:1. Fix the background, not the text: darken the top stops and move the bright band down so it sits behind surfaces instead of behind labels.

## Computing contrast

```js
// sRGB hex to relative luminance, then WCAG contrast ratio
const lum = (hex) => {
  const [r, g, b] = [1, 3, 5].map((i) => parseInt(hex.slice(i, i + 2), 16) / 255)
    .map((c) => (c <= 0.04045 ? c / 12.92 : ((c + 0.055) / 1.055) ** 2.4));
  return 0.2126 * r + 0.7152 * g + 0.0722 * b;
};
const contrast = (a, b) => {
  const [hi, lo] = [lum(a), lum(b)].sort((x, y) => y - x);
  return (hi + 0.05) / (lo + 0.05);
};
contrast("#FCF8F1", "#E6964F"); // 2.25
```

For text over a translucent surface, composite first: each channel is `alpha × surface + (1 − alpha) × background`, then measure against the result. For a gradient, measure against the lightest and the darkest color the text can sit over.

## In CSS

```css
:root {
  --atmosphere: linear-gradient(
    in oklch to bottom,
    oklch(0.66 0.10 285) 0%,
    oklch(0.78 0.08 40) 42%,
    oklch(0.74 0.13 60) 62%,
    oklch(0.30 0.05 50) 100%
  );
}

.screen {
  background: #8c89cd linear-gradient(to bottom, #8c89cd, #e5a691 42%, #e6964f 62%, #422616); /* fallback */
  background: var(--atmosphere);
  min-height: 100dvh;
}

/* grain against banding */
.screen::after {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  opacity: 0.035;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 0.5 0 0 0 0 0.5 0 0 0 0 0.5 0 0 0 1 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
```

The background covers the whole viewport, behind the status bar and the tab bar. Content stays inside the margins and safe areas.

Put the stops and the roles in the project's token file as semantic tokens. Components reference roles, never stops.

## In Figma

- Apply the gradient as a linear fill on the screen's root frame, top to bottom, with the stop positions from the table.
- Figma interpolates gradients in sRGB. Where a transition goes muddy, add a middle stop sampled from the OKLCH version.
- For grain, add a noise or texture effect if the file's Figma version has one, or a rectangle filled with a noise image at 3 to 4 percent opacity as the top layer of the background, locked.
- Create color variables or styles for the roles and bind fills to them. Leave no raw hex on text layers.
- Delete the old background ellipses and glows. Do not hide them.

## Content-led atmosphere

When the atmosphere is the content's own color:

1. Take the current image and scale it up to cover the screen.
2. Blur it heavily, 60 to 100px, and lower its saturation slightly.
3. Lay a dark scrim over it, 30 to 50 percent, so text contrast holds whatever the image is.
4. Sample the accent from the image's most saturated region, then check it against the scrimmed background.

Measure text against the scrimmed result with the brightest image you expect, not the sample one.
