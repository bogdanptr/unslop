# Example: sleep summary

A full run of the pipeline on one AI-generated screen. The source was a screenshot only, so the result is a single HTML file.

- Before: [before.png](before.png)
- After: [after.html](after.html), open it in a browser

## Unslopped: sleep summary

**Mode** full · **Source** `before.png`, assumed width 390 · **Result** `after.html`

**Direction** A night's sleep runs from going to bed to waking up, so the screen is the sky just before sunrise and the main figure is an arc from moon to sun.

### What changed

| Before | After | Why |
| --- | --- | --- |
| Score ring, duration, four tiles, a chart and a tip at similar weight | One hero, a quiet metric group, one line of text | The screen answers one question: how did I sleep |
| A ring around the score | An arc from bedtime to wake time with the duration at its center | A ring fits any app. The arc is the night |
| Indigo accent on near-black, violet gradient button | A pre-dawn sky, accent taken from its sunrise stop | Every color now has the same source |
| Bordered cards, icons in tinted tiles, four hues | Borderless dark glass, bare icons in the label color | Fewer boxes, the values read first |
| Inter semibold throughout | Manrope, hero at weight 300, units smaller and lighter | The big text stops shouting |
| Green pill for the delta | Neutral chip with an arrow | Direction is carried by the arrow, not by a tint |
| Full-width gradient button under the content | Round `Start` at the center of the metric group | In thumb reach, part of the composition |
| 5 tabs: Home, Stats, Sounds, Journal, Profile | 4 tabs: Today, Stats, Sounds, Journal. Profile opens from the avatar | One fewer destination, a first tab named for what it shows |

### Content ledger

| ID | Element | Disposition | Where it is now |
| --- | --- | --- | --- |
| C1 | `Good morning, Alex` | keep | Caption above the hero |
| C2 | `Here's your sleep summary` | cut | Filler: no data, no action |
| C3 | Avatar `AK` | keep | Top right, now also the way to Profile |
| C4 | `Score` `82` | restyle | Chip under the hero |
| C5 | `7h 42m`, `Last Night's Sleep` | keep | Hero center |
| C6 | `24 min vs avg`, up | restyle | Neutral chip with an arrow |
| C7 | `Deep Sleep` `1h 48m` | keep | Metric group |
| C8 | `REM` `1h 31m` | keep | Metric group |
| C9 | `Avg Heart Rate` `58 bpm` | keep | Metric group |
| C10 | `Awake` `12 min` | keep | Metric group |
| C11 | `This Week` chart, 7 bars, `View all` | demote | Stats tab |
| C12 | `Sleep Tip` and its sentence | keep | Plain text under the metrics. Source unknown, so treated as live data |
| C13 | `Start Sleep Tracking` | relabel | `Start`, accessible name `Start sleep tracking` |
| C14 | Tab `Home` | relabel | `Today` |
| C15 to C17 | Tabs `Stats`, `Sounds`, `Journal` | keep | Tab bar |
| C18 | Tab `Profile` | demote | Avatar button |

**Needs data.** `sleep.bedtime`, `sleep.wakeTime`: the arc's ends show `--:--`. The source screen has only a duration.
**Assumed.** The Stats tab holds the weekly chart. The source links there with `View all`, but a screenshot cannot show it.
**Proposed, not applied.** Moving Sounds into the tracking session, and sentence case for the metric labels.
**Not verified.** Narrow widths and large text settings (the mock is a fixed 390 by 844 frame), real action wiring, states other than the default.

## The same run in Figma

The screen was also built as a Figma frame and run through `unslop-figma`. The source frame was cloned, the clone restyled, and the source left as it was: 109 layers and 33 text strings before and after.

- All 22 kept strings are the original text layers, moved into the new structure. Two changed characters, both recorded relabels: `Start Sleep Tracking` to `Start`, `Home` to `Today`. Two new text layers are the `--:--` placeholders.
- Colors, radius and gaps are bound to a variable collection made for the restyle. No text layer has a raw fill.
- Contrast was measured again on the Figma gradient: every text layer is 5.3:1 or better.
- Not done in Figma: the grain layer, and binding the arc's own colors to variables.

## What the verification caught

The first build looked right and failed measurement. Secondary text on the transition into the sunrise band measured 2.6:1 to 3.9:1 in four places. The fix was a darker sky overhead, stronger glass and stronger secondary text, after which every text pair measured 5.2:1 or better.

An independent critic then returned `Ship` with findings. Fixed since: the `Start` button could cover a metric label that wrapped, the tab bar had a shadow the tiles did not, the button sat inside a `<dl>`, and a few colors were repeated as literals. Still open: the four tiles remain a uniform 2 by 2 grid.
