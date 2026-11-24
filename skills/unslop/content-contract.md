# Content contract

The record of what a screen contains, written before any restyling and checked after it. It is the reason a reskin can be bold without being wrong.

## What goes in it

One row per element that carries information or does something. Decoration with no information, such as a background blob, is listed once as a group.

| Field | What to write |
| --- | --- |
| ID | A short stable id, `C1`, `C2`, in reading order |
| Element | What it is: metric, label, chart, button, tab, image, list row |
| Content | The exact string or value, copied character for character, including units, punctuation and capitalization |
| Source | Where it comes from: a prop, a variable, a query field, a hardcoded string, a Figma text layer. `unknown` when you cannot tell |
| Action | What it does and where it goes: a route, a handler name, a prototype link. `none` for static content |
| States | The states the source draws or codes: empty, loading, error, selected, disabled |

A short example, from a sleep app's home screen. The same table is written for any view: on a billing table each column header, each row's fields, each filter and each row action is a row or a grouped row.

| ID | Element | Content | Source | Action | States |
| --- | --- | --- | --- | --- | --- |
| C1 | Greeting | `Good morning, Alex` | `user.firstName` | none | |
| C2 | Score | `82` label `Score` | `sleep.score` | none | loading |
| C3 | Duration | `7h 42m` label `Last Night's Sleep` | `sleep.durationMin` | none | |
| C4 | Delta | `24 min vs avg` | `sleep.deltaMin` | none | positive, negative |
| C5 | Metric | `Deep Sleep` `1h 48m` | `sleep.deepMin` | none | |
| C9 | Chart | `This Week`, 7 bars M to S, Sunday highlighted, link `View all` | `week[]` | `/stats` | |
| C10 | Tip | `Sleep Tip` + one sentence | hardcoded | none | |
| C11 | Primary button | `Start Sleep Tracking` | | `startTracking()` | |
| C12 | Tab bar | `Home` `Stats` `Sounds` `Journal` `Profile` | | 5 routes | Home selected |

Charts list their data: how many points, what each axis is, which point is highlighted. A chart recorded as "bar chart" cannot be checked later.

## Rules that hold in every mode

- **Values are verbatim.** `7h 42m` stays `7h 42m`. Splitting it into styled spans is fine. Rounding it, reformatting it to `7.7 h` or changing its unit is not, unless the user asks.
- **No invented content.** No new metric, testimonial, feature, badge, date or name. Realistic-looking filler is the most damaging kind, because nobody notices it is fake.
- **Placeholder data stays as it was.** `Alex`, `Lorem ipsum` and sample numbers in the source are the source. Do not improve them.
- **Wrong-looking data is reported, not corrected.** When source values contradict each other, such as an amount that does not match the rate beside it or a total that is not the sum of its rows, carry them over as written and say so in the report. The error may be in the sample data or in your reading.
- **Derived values are allowed only when computable.** A percentage from two contract values, or a field that already exists in the data model, may be shown. A value that looks plausible but has no source is invented.
- **Missing data is marked, not faked.** When a new figure needs a value the source lacks, such as a bedtime for a sleep arc, build it with a clearly marked placeholder, list it under **Needs data** and name the field it expects.
- **Actions keep their destination.** A restyled button calls the same handler. A renamed tab opens the same route.
- **States survive.** If the source has an empty or error state, the result has one in the new style. A state the source never had is not yours to add; list it as missing.
- **Images and logos are kept.** Crop, mask and place them freely. Do not replace, regenerate or recolor a logo.

## Dispositions

Every row ends with exactly one:

| Disposition | Meaning | Allowed in `reskin` |
| --- | --- | --- |
| `keep` | Same element, same place in the hierarchy, new look | Yes |
| `restyle` | Same content in a different visual form, such as a ring becoming an arc or a pill becoming plain text | Yes, except chart form |
| `merge` | Two rows now shown as one element. Both values still visible | Yes |
| `move` | Same element, different position or level | No |
| `relabel` | Interface label reworded. Never data, never user content | No |
| `demote` | Removed from this view, reachable one step away. Name the step | No |
| `cut` | Removed from this view. Must pass the test below | No |

## When something may be cut

Cutting is how a screen gets a focus, and it is the riskiest thing this skill does. An element may be cut only when one of these is true:

1. **It duplicates** information another element on the same screen already shows.
2. **It is filler**: generic advice, a decorative illustration, a marketing line, anything with no data behind it and no action.
3. **It is secondary and lives elsewhere**: a full view of it already exists one tap away, and this screen keeps the entry point. This is a `demote`, and the ledger names where.

Anything bound to live data with no other home is never cut. Demote it behind a disclosure, a detail view or a "See all" row instead.

In code, a `cut` or `demote` of anything with a data binding or a handler is proposed in the report and applied only when the user asked for a full rework or approves it. In a Figma copy, apply it and list it.

## The ledger

The contract with a disposition and a location per row. It goes in the report in full:

| ID | Element | Disposition | Where it is now |
| --- | --- | --- | --- |
| C2 | Score `82` | restyle | Chip under the hero arc |
| C3 | Duration `7h 42m` | keep | Center of the hero |
| C9 | Weekly chart | demote | Stats tab, which already shows it |
| C10 | Sleep tip | cut | Filler, hardcoded, no data |
| C11 | `Start Sleep Tracking` | relabel | `Start`, center of the metric grid, same handler |

A row missing from the ledger is a bug in the reskin, whatever the result looks like.

## When the source is unknown or a screenshot

- **`Source: unknown` is treated as live data.** A tip that might be hardcoded might also be personalised. If you cannot tell, it is kept or demoted, never cut as filler.
- **A screenshot contract is a transcription, and transcriptions have errors.** Read the image twice. Record icons, chart shapes and the selected state as well as strings. Mark any character you are not sure of. Leave `Source`, `Action` and `States` as `unknown` instead of dropping the columns.
- **A demote must point at something you can see.** "The Stats tab already shows the weekly chart" is checkable in a codebase or a multi-frame file. From one screenshot it is an assumption. Apply it only when the source itself points there, such as a `View all` link beside the chart, and list it under **Assumed** in the report so the user can confirm.
- **Changing an interface label's capitalization is a `relabel`.** `Deep Sleep` to `Deep sleep` changes the string. Uppercase or lowercase applied with a case transform leaves the string as written and is styling.
