# Chart swaps

Generic forms and what to draw instead, by the story the data tells. Each entry lists the data the form needs, so missing values are caught before drawing.

## By story

| The story | Generic form | Forms with a point of view | Needs |
| --- | --- | --- | --- |
| A span between two moments | Ring, duration in a card | An arc or a strip from start to end with both ends labeled | Start, end, or one of them plus the duration |
| Progress toward a goal | Percentage ring | A vessel filling, a path with a marker, a bar with the goal line drawn | Current value, goal |
| A level within a range | Gauge, score ring | A scale with the usual band shaded and a marker on it | Value, minimum, maximum, optionally the usual range |
| Change over time | Small multicolor bar chart | One line, drawn large, with the latest point labeled | A series with dates |
| Parts of a whole | Donut with a legend | One segmented bar with direct labels, or a ranked list with proportional bars | The parts. They must sum to the whole |
| A comparison with usual | Green or red pill | The value with a thin marker showing the average on the same scale | Value, average |
| A position on a route | Stat cards for distance and pace | The route or the elevation profile with the current point | Coordinates or an elevation series |
| A rhythm across the week | Seven gray bars, one highlighted | Seven dots or bars sized by value, today marked, days labeled | Seven values |
| A streak | A flame icon and a number | A row of the last days, filled or empty | Per-day completion |

## Drawing a span as an arc

The sleep example, as SVG. The arc is always the same shape. Its ends carry the two times.

```html
<svg viewBox="0 0 320 200" role="img" aria-label="Slept 7h 42m, from 11:24 PM to 7:06 AM">
  <defs>
    <linearGradient id="span" x1="0" x2="1">
      <stop offset="0" stop-color="var(--arc-start)" />
      <stop offset="1" stop-color="var(--arc-end)" />
    </linearGradient>
  </defs>
  <!-- a 200 degree arc, radius 120, centered at 160,160 -->
  <path d="M 41.8 180.8 A 120 120 0 1 1 278.2 180.8"
        fill="none" stroke="url(#span)" stroke-width="10" stroke-linecap="round" />
</svg>
```

- Stroke width 8 to 12 at this size, round caps.
- The gradient runs along the arc from the atmosphere's cool stop to its warm stop.
- The start and end glyphs sit on the arc's ends, with their time labels outside the arc.
- The value sits at the arc's center, the label under it.
- Give the SVG a text alternative that states the values. The times and the duration are also real text in the DOM.

When the arc shows a span, its shape is fixed and the labels carry the data. When it shows progress, its drawn length is proportional: set `stroke-dasharray` to the path length and `stroke-dashoffset` to `length × (1 − value ÷ goal)`.

## Drawing a level on a scale

```html
<div class="scale" role="img" aria-label="Resting heart rate 58 bpm, usual range 55 to 62">
  <div class="scale-band"   style="inset-inline-start: 37.5%; inline-size: 17.5%"></div>
  <div class="scale-marker" style="inset-inline-start: 45%"></div>
</div>
```

Positions are `(value − min) ÷ (max − min)`. With a scale of 40 to 80, a value of 58 sits at 45 percent and a 55 to 62 band starts at 37.5 percent and is 17.5 percent wide. Compute them from the data. Never place a marker by eye.

## Drawing parts as one bar

```html
<div class="parts" role="img" aria-label="Deep 1h 48m, REM 1h 31m, light 4h 11m, awake 12m">
  <span style="flex: 108"></span>
  <span style="flex: 91"></span>
  <span style="flex: 251"></span>
  <span style="flex: 12"></span>
</div>
```

Use the raw values as `flex` weights so proportions are exact. Gap 2 between segments, round the outer ends only. Steps of one hue from the palette, darkest for the first part, not one hue per part.

Only draw parts of a whole when the parts sum to the whole. Four sleep stages that sum to the night can be one bar. Four unrelated stats cannot.

## In Figma

- Draw arcs with an ellipse's arc controls, or a vector path with a round-capped stroke, not with a rotated half-circle mask.
- Keep the value, the unit and the labels as text layers, never outlined, so the content can still be checked against the contract.
- Size proportional marks from the numbers. Name the layer with the value it encodes, such as `Deep 108min`, so the next reader can verify it.
