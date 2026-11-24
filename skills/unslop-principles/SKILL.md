---
name: unslop-principles
description: The design fundamentals a senior product designer applies to any interface - hierarchy, grouping, alignment, contrast, consistency, restraint, rhythm, affordance, density and detail - each with a test that can be run on a screen. Use when judging or restyling any UI, when a design feels off and nobody can say why, when asked what makes an interface look premium or design-led, or as the shared basis for every unslop pass.
---

# Design principles

This skill is the judgment the other skills assume. It states the laws that hold for every interface, whatever the product, and gives each one a test you can run on a screen. A restyle that follows every value in the pass skills and fails these tests is still not good.

It holds no values. Spacing and structure are in `unslop-layout`, containers and controls in `unslop-surfaces`, figures and tables in `unslop-dataviz`, type in `unslop-typography`, color in `unslop-color`, navigation and wording in `unslop-navigation`. The idea a restyle is built on comes from `unslop-direction`, and the pipeline is `unslop`.

## The principles decide, the pass skills give the numbers

Each principle below is a question with a yes or no answer for a given screen. Where the answer is no, the owner named beside it has the rule and the value that fixes it. When two pass rules pull in different directions, the principle decides which one gives way.

Run the tests on a render, not on code. Most of them need only a screenshot and ten seconds.

In `reskin` mode the principles still apply, limited to what styling can change: tone, weight, spacing, surfaces. Structure stays.

## 1. One thing is first

Every view has an order of reading: first, second, third, then everything else. The eye should land on the first thing without help.

**Test.** Blur the screenshot or shrink it to a thumbnail. One region dominates. Then ask someone, or yourself after looking away, what the screen is for. The answer matches the view's job in the brief.

Hierarchy is built from position, size, tone, weight and space, in roughly that order of strength. Use the fewest that make the order clear. Three signals on one element, such as large and bold and colored, means the others are too loud. Owner: `unslop-layout` for position and space, `unslop-typography` for size, tone and weight.

## 2. What belongs together sits together

Distance is meaning. Things close together read as one group, and the gap between groups is clearly larger than the gap inside them. Space does this before any line or box does.

**Test.** Remove every border and background in your head. The groups are still obvious. If they are not, the spacing is wrong and the boxes were hiding it. Owner: `unslop-layout`.

## 3. Few edges, shared by everything

Elements line up on a small number of vertical and horizontal lines. Every edge that is almost aligned with another, off by 2 or 4, reads as a mistake.

**Test.** Draw a vertical line down each leading edge in the view. Count the lines. A typical view needs two to four. Owner: `unslop-layout`.

## 4. Different things look clearly different, same things look the same

A difference the eye can barely see is noise. Two sizes 1px apart, two grays 3 percent apart, two radii of 10 and 12: each should be one value, or far enough apart to mean something.

The other half is consistency. The same kind of thing looks the same everywhere: every primary button, every field, every row, every icon. One of each.

**Test.** List the distinct font sizes, weights, text colors, radii, shadows and button styles in the view. Each list is short, and every entry has a job you can name. Owner: `unslop-typography`, `unslop-surfaces`, `unslop-color`.

## 5. Restraint

A premium interface is mostly a matter of what is absent. One accent color. One or two typefaces. One material. One signature element. A few sizes. Everything added after that has to justify itself against the calm it costs.

**Test.** Cover the element and look again. If the screen is no worse, the element goes: a border, an icon, a badge, a subtitle, a shadow, a gradient, a divider. Owner: whichever pass owns the element. What may be removed when it is content, not decoration, belongs to `unslop`'s contract.

## 6. Rhythm

Spacing, sizes and proportions come from a small set of steps, so the view has a pulse and not a series of one-off decisions. Repeated elements repeat exactly.

**Test.** Measure the gaps. They are on the scale, and the same relationship has the same gap wherever it appears. Owner: `unslop-layout`.

## 7. Controls look like controls

Anything that can be pressed looks pressable, and nothing else does. A primary action is the most prominent control in the view. Text that is a link looks different from text that is not. Every control has its states: rest, hover where there is a pointer, pressed, focused, disabled, loading.

**Test.** Point at each interactive element and each static one. A stranger sorts them correctly. Tab through the view: focus is always visible. Owner: `unslop-surfaces` for the shapes and states, `unslop-navigation` for wording.

## 8. Fewer choices, bigger targets

Every option added slows every decision. Offer the few things people do here, and put the rest one step away. The more often a control is used, the larger and closer it is. A touch target is at least 44 by 44, and a pointer target at least 24 by 24 with space around it.

**Test.** Count the actions visible at once. Name the one used most. It is the easiest to reach. Owner: `unslop-navigation` for how many, `unslop-layout` for where.

## 9. Density fits the task

Calm is not the same as empty. A screen someone glances at once a day should be sparse. A screen someone works in for hours should be dense, even and quiet, with small type, tight rows and no decoration. Applying the first treatment to the second kind of screen is the most common way a restyle makes a product worse.

**Test.** Name how long a person looks at this view and what they do there. The amount on screen matches. Owner: `unslop-direction` for the kind of screen, `unslop-layout` for the structure.

## 10. Optical beats mathematical

Centered by the numbers is not always centered to the eye. An icon beside text aligns to the text's visual middle. A triangle in a circle shifts toward its point. Round shapes overshoot. Large type needs tighter tracking, and light text on dark looks heavier than the same weight dark on light.

**Test.** Look at each icon and label pair, each centered element and each large line of type. Nothing looks off-center or loose, whatever the numbers say. Owner: `unslop-surfaces` for icons, `unslop-typography` for type.

## 11. It is designed with the real content

A design that only works with short names, round numbers and three items is a mockup. Real content has a 40-character name, a value of zero, an empty list, an error, a number with five digits.

**Test.** Put the longest plausible string in each label, an empty state in each list, and a large and a zero value in each figure. Nothing clips, overlaps or collapses. Owner: `unslop-verify` runs this, `unslop-layout` fixes it. Test content is for checking only and is never left in the result.

## 12. Finished means every part

The difference between good and premium is the last tenth: the states nobody asked for, the focus ring, the 1px that was off, the icon whose stroke did not match, the second theme, the narrow width. A view with one excellent region and five default ones reads as default.

**Test.** Pick the least important element on the screen and look at it closely. It was considered too.

## What premium means, in decisions

The qualities the author of this collection treats as good taste, each with a check, are in [taste.md](taste.md). Use them as the tiebreaker when the rules leave a choice open.

"Premium" and "modern" are not instructions. These are:

| It reads as generic when | It reads as considered when |
| --- | --- |
| Every section has the same weight | One thing leads and the rest is visibly quieter |
| Groups are made with boxes | Groups are made with space |
| Six font sizes close together, most text semibold | Four or five sizes with clear steps, weight used sparingly |
| Neutral grays with a default accent everywhere | Tinted neutrals with one accent used for one purpose |
| Borders, shadows and fills all at once | One way of separating surfaces |
| Icons decorate every label | Icons appear where they speed recognition |
| Color is used to make things lively | Color is used to mean something |
| Type at default tracking and line height | Large type tightened, long text given room |
| Everything is centered, or nothing lines up | A few shared edges |
| Controls from the library, untouched | One field, one button, one row style, tuned to the type |
| It looks right with the sample data | It holds with long, empty and extreme data |
| The idea could belong to any product | Something in it could only be this product |

## Before you finish

| You notice | Fix |
| --- | --- |
| Blurred, no region dominates | Principle 1. `unslop-layout` |
| An element that is large, bold and colored at once | Remove signals until one is left |
| Groups that only read as groups because of their boxes | Fix the spacing, then remove the boxes |
| An edge 2 to 4 off a neighbouring edge | Put both on one line |
| Two values of one property closer than a clear step | Merge them or separate them |
| The same kind of control styled two ways | One style |
| An element whose removal changes nothing | Remove it |
| A static element that looks pressable, or a control that does not | Fix the affordance |
| A control with no focus, hover or disabled state | Add the states the source had, in the new style |
| A work view thinned out to look calm | Restore the density |
| An icon or shape that is centered by numbers and looks off | Nudge it by eye |
| A layout that breaks with a long name, an empty list or a large number | Fix it, then take the test content back out |
| One polished region beside untouched default ones | Finish the rest |
