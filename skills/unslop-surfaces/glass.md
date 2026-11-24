# Glass

Recipes for the glass material in CSS and in Figma, over dark and light backgrounds.

## Over a dark or saturated background

```css
:root {
  --glass-fill: rgb(255 255 255 / 0.10);
  --glass-line: rgb(255 255 255 / 0.12);
  --glass-highlight: rgb(255 255 255 / 0.22);
  --glass-blur: 24px;
}

.glass {
  background: var(--glass-fill);
  -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(160%);
  backdrop-filter: blur(var(--glass-blur)) saturate(160%);
  border: 1px solid var(--glass-line);
  box-shadow:
    inset 0 1px 0 var(--glass-highlight),
    0 8px 32px rgb(0 0 0 / 0.12);
}

@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .glass { background: color-mix(in oklab, var(--color-surface) 88%, transparent); }
}
```

Tailwind, with arbitrary values where no utility exists:

```html
<div class="bg-white/10 backdrop-blur-xl backdrop-saturate-150 border border-white/[0.12]
            shadow-[inset_0_1px_0_rgb(255_255_255/0.22),0_8px_32px_rgb(0_0_0/0.12)]">
```

## Over a bright region

White-tinted glass over a bright part of the background brightens it further, so white text loses contrast. Tint the glass dark, in a deep tone of the background's own hue:

```css
.glass-dark {
  background: rgb(40 22 12 / 0.45);            /* a dark tone of the background hue */
  backdrop-filter: blur(24px) saturate(160%);
  border: 1px solid rgb(255 255 255 / 0.10);
  box-shadow: inset 0 1px 0 rgb(255 255 255 / 0.16);
}
```

How dark depends on the text it carries. Measured over a peach band at OKLCH lightness 0.74, near-white text reaches about 3.4:1 on this tint at 0.24 opacity, enough for large text only, and about 5.3:1 at 0.45, enough for small text. Measure against your own background before settling on a value.

Use one glass tint per screen. If the surface spans a bright region and a dark one, the dark tint works over both.

## Over a light background

```css
.glass-light {
  background: rgb(255 255 255 / 0.55);         /* 0.45 to 0.65 */
  backdrop-filter: blur(24px) saturate(180%);
  border: 1px solid rgb(255 255 255 / 0.60);
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / 0.80),
    0 8px 32px rgb(0 0 0 / 0.06);
}
```

Text on light glass is the dark text color.

## Chips and controls on glass

Elements inside a glass surface take a stronger fill and no blur of their own:

```css
.glass .chip { background: rgb(255 255 255 / 0.12); border: 0; }
```

## In Figma

On the frame that becomes glass:

| Property | Value |
| --- | --- |
| Fill | White at 10 percent, or a dark tone of the background hue at 25 to 45 percent over bright regions |
| Effect | Background blur, 24. In the Plugin API a `BACKGROUND_BLUR` effect with `radius: 24` |
| Stroke | 1px, inside. A linear gradient from white 30 percent at the top to white 5 percent at the bottom reads as a lit edge. A flat white 12 percent also works |
| Effect | Inner shadow, y 1, blur 0, white 22 percent, for the top highlight |
| Effect | Drop shadow, y 8, blur 32, black 12 percent |

Background blur in Figma only shows when the fill is partly transparent. A frame with a 100 percent fill and a background blur renders as a solid.

The frame must sit above the background in the layer order and must not clip the background into itself. Check the render after applying it.

## Performance

`backdrop-filter` is repainted when anything behind it changes. Keep glass off long scrolling lists of many items. One blurred container that holds the list is fine. A blurred surface per row is not.
