# Taste reference

What the author of this collection points to as good taste, written as qualities you can check. They come from interfaces the author marked as reference quality. They are a tiebreaker when the pass skills leave a choice open, never a template: the qualities transfer, the screens do not.

Where a reference breaks an explicit rule in a pass skill, the rule wins. The references are liked for the qualities below, not for every detail in them.

## The qualities

| Quality | What it looks like | Check | Owner of the rule |
| --- | --- | --- | --- |
| Color has a place | The brand color fills one region at full strength, usually the top of the view, and the rest is white or near-white. It is not sprinkled across the screen | Squint: one colored region, one neutral region | `unslop-color`, **A bleed joins the color to the page** |
| The color meets the page softly | The colored region fades into the page instead of ending at a line, and a content surface sits across the transition | No hard edge between the colored region and the page | `unslop-color` |
| Three colors | The brand hue, a near-black and white. Near-black carries the second level of emphasis, so the brand color does not have to | Count hues: one. Count emphasis levels: brand, near-black, neutral | `unslop-color`, **Near-black is the second emphasis** |
| White controls on color | Buttons on the colored region are white with dark labels, not darker or lighter shades of the color | Every control on the field is the same white | `unslop-color`, **When the accent is a field** |
| Two levels of depth, softly | A white surface on the page with a very soft shadow, and inside it at most one quieter inset panel. No borders doing the same job | Count nesting levels: two at most | `unslop-surfaces` |
| Dense and calm at once | Many things on one screen, in small even type with tight rows, and still easy to scan | Rows are 44 to 56 tall, text 11 to 14, and nothing feels crowded | `unslop-layout`, `unslop-typography` |
| One strong figure | The main number is the largest text by a clear margin and has open space around it | It is at least twice the size of the next text | `unslop-typography` |
| Rows scan from the left | List rows open with a small leading mark of one style, then name and detail, with the value at the trailing edge | Every row has the same three parts in the same places | `unslop-surfaces`, `unslop-dataviz` |
| Navigation floats | The bar is its own surface, inset from the edges, with a quiet capsule on the current item | It does not touch the screen edges | `unslop-surfaces`, `unslop-navigation` |
| Small, exact details | Icons of one weight, even gaps, one label style. Nothing is loud except the one figure and the one color region | Zoom to 200 percent on any corner: it holds | `unslop-principles` |

These qualities are not limited to consumer or mobile screens. On a dashboard or a form the colored region is the header band, the strong figure is the lead number in it, and the depth is the working surface sitting on the page.

## How to use it

- After `unslop-direction` writes the brief, read the table once. If the brief contradicts a quality without a reason from the product, reconsider that dial.
- When a pass offers two valid options, take the one the table favors.
- In `unslop-verify`, a result that passes every rule and shows none of these qualities is correct and plain. Say so.

Add a row when the author marks a new reference, and only for a quality that would apply to products the reference has nothing to do with.
