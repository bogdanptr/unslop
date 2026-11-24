# Slop tells

The catalog. Each tell has what it looks like, how to find it in code and in Figma, and the skill that owns the fix. A pattern is a tell only when nothing about the product explains it.

## Tier 1: identity

| Tell | Looks like | In code | In Figma | Owner |
| --- | --- | --- | --- | --- |
| Default indigo-violet palette | Indigo or violet accent, often as a gradient, on slate or navy | `#6366F1`, `#4F46E5`, `#8B5CF6`, `#7C3AED`, `#A855F7`; `indigo-500`, `violet-500`, `purple-600`; `from-indigo-* to-purple-*` | Fills with an HSL hue of 235 to 275 degrees and no color variable or brand style behind them | `unslop-color` |
| Default dark base | Navy-black page with slightly lighter navy cards | `#0F172A`, `#111827`, `#1E293B`, `#0B1120`; `slate-900`, `gray-900`, `zinc-950` | Frame fill and card fills 3 to 6 percent apart in lightness, same cool hue | `unslop-color` |
| Default light base | White cards on `gray-50` with gray borders | `#F9FAFB`, `#F3F4F6`, `#E5E7EB`; `bg-gray-50`, `border-gray-200` | The same three grays on every frame | `unslop-color` |
| Background means nothing | A flat fill, or decorative blobs and glows unrelated to the product | `blur-3xl` circles, `radial-gradient` in the accent color at a corner | Blurred ellipses behind content named `Glow`, `Blob`, `Ellipse 12` | `unslop-color` |
| Generic main figure | The main number sits in a ring, a donut or a plain card | An SVG `circle` with `stroke-dasharray` around a number; a `RadialBar` or `Doughnut` as the first chart | An ellipse with an arc stroke and a centered number | `unslop-dataviz` |
| Default typeface, one voice | Inter, Roboto, Poppins or the system face for everything | `font-family: Inter`; `font-sans` with no custom family; a single `next/font` import | One font family across all text layers | `unslop-typography` |
| Everything bold | Headings, numbers and labels all at 600 to 700 | `font-semibold` or `font-bold` on most text nodes | Semi Bold or Bold on more than half the text layers | `unslop-typography` |

## Tier 2: structure

| Tell | Looks like | In code | In Figma | Owner |
| --- | --- | --- | --- | --- |
| No focal point | Three or more sections of similar size, no dominant element | Sibling sections with the same padding and heading style | Top-level children of similar height | `unslop-layout` |
| Everything in a card | Every group has a rounded rectangle with fill and border | The same `rounded-xl border bg-*` wrapper on every section | Every auto-layout group has a fill, a stroke and a radius | `unslop-layout` |
| Card in a card | A bordered card holding bordered cards | Nested elements that both carry `border` and `rounded-*` | A filled, stroked frame whose children are filled, stroked frames | `unslop-surfaces` |
| Stat-card row leads | A row of three or four equal stat cards is the first thing on a dashboard, above the content the view exists for | A `grid-cols-4` of `StatCard` as the first child of the page | Four equal frames across the top of the content area | `unslop-layout` |
| Uniform metric grid | A 2 by 2 or 3 by N grid of identical stat tiles: icon, label, value | `grid grid-cols-2 gap-*` with one repeated component | Four or more instances of one tile component in a grid | `unslop-layout` |
| The filler card | A tip, a quote, a "Did you know", a generic insight | A hardcoded string in a card with a lightbulb or sparkle icon | A card whose text is not bound to anything and reads like advice | `unslop-layout` |
| Full-width gradient call to action | A wide gradient button pinned under the content | `w-full bg-gradient-to-r` on a button | A full-width button with a linear gradient fill | `unslop-surfaces`, `unslop-layout` |
| Three feature cards | A marketing section of exactly three equal cards: icon tile, bold title, two gray lines | `grid md:grid-cols-3` with one repeated card | Three identical frames in a row under a centered heading | `unslop-layout` |
| Centered everything | Every section is a centered heading, a centered subtitle and a centered block | `text-center mx-auto max-w-2xl` on every section | Every section's children centered | `unslop-layout` |
| The stacked landing page | Hero, logo strip, three features, testimonials, pricing, call to action, each built the same way | Section components in that order with the same padding and heading block | Equal-height sections with identical header blocks | `unslop-layout` |
| Sidebar of everything | Ten or more navigation items, each with an icon, the first called Dashboard | A `navItems` array of ten or more entries | A sidebar with ten or more rows | `unslop-navigation` |
| A card around every form group | Each group of two or three fields sits in its own bordered card with a title and a description | `Card` with `CardHeader` and `CardContent` repeated down a settings page | Stacked bordered frames each holding a few fields | `unslop-surfaces` |
| Five tabs because five fit | A full tab bar with vague names: Home, Explore, Profile | Five or more tab routes; a tab named `Home` | A tab bar with five items | `unslop-navigation` |
| Greeting as headline | "Good morning, Alex" or "Welcome back" is the largest text on the screen | The greeting in the `h1` | The largest text layer is the greeting | `unslop-layout` |
| Section header on every section | Each block has a title and a "View all" link | A repeated `SectionHeader` with a title and a link | A title and link row above every group | `unslop-layout` |

## Tier 3: detail

| Tell | Looks like | In code | In Figma | Owner |
| --- | --- | --- | --- | --- |
| Boxed icons | Each icon sits in a tinted rounded square or circle | A `div` with `rounded-lg bg-*-500/10 p-2` wrapping an icon | A frame with a 10 to 20 percent tint fill around an icon instance | `unslop-surfaces` |
| Rainbow metrics | Each stat has its own hue: blue, purple, green, orange | Four accent colors mapped to array index | Sibling tiles whose icons have unrelated fills | `unslop-color` |
| Border and fill and shadow together | A card separated from the page three ways at once | `border` with `bg-*` with `shadow-*` on one element | A stroke, a contrasting fill and a drop shadow on one frame | `unslop-surfaces` |
| Glow under the button | A colored blur beneath the primary action | `shadow-lg shadow-indigo-500/50`; `box-shadow` in the accent color | A drop shadow in the accent hue with a blur above 16 | `unslop-surfaces` |
| The green delta pill | A small green rounded badge with an arrow and a percentage | `bg-green-500/10 text-green-400 rounded-full px-2` | A pill with a green tint fill | `unslop-dataviz` |
| One highlighted bar | Gray bars with the last one in the accent color, no values | A bar list where the last index gets the accent class | Seven rectangles, six gray | `unslop-dataviz` |
| Boxed table | A table with an outer border, a filled header, lines on every side of every cell, sometimes zebra stripes as well | `border` on `table`, `th` and `td`; `divide-x` with `divide-y` | Stroked cells in a stroked frame | `unslop-dataviz` |
| Badge in every row | A filled colored status pill in each table or list row | A `Badge` with a color variant per status in every row | A tinted pill in every row | `unslop-dataviz` |
| Default chart | The chart library's first render: its palette, a legend, a full grid, a tooltip box | `recharts` or `chart.js` with no theme; `CartesianGrid` and `Legend` left in | A chart with gridlines, a legend and several unrelated hues | `unslop-dataviz` |
| Library defaults untouched | Inputs, buttons and dialogs exactly as the component library ships them | Unmodified `shadcn/ui`, MUI or Chakra theme; `ring-offset-background` everywhere | Fields with a gray stroke and a blue focus style | `unslop-surfaces` |
| The eyebrow pill | A small rounded badge above a headline, often with a sparkle or "New" | A `rounded-full border px-3 py-1 text-xs` element before the `h1` | A pill above the headline | `unslop-typography` |
| Subtitle under everything | Every heading has a gray sentence under it that restates it | A `text-muted-foreground` paragraph after each heading | A secondary text layer under every title | `unslop-layout` |
| Dot-separated text | Short facts strung on one line with a middle dot or bullet between them: `Instant · Free · Secure`, `3 min read · Design · Today` | `·`, `•`, `&middot;`, `&bull;` or a 3 to 4px round element between inline spans | A `·` or `•` character, or a tiny ellipse, between text layers in a row | `unslop-typography` |
| Mixed control treatments | Controls of one kind drawn different ways in the same view: a bare icon button beside one in a filled circle, an avatar with no ring beside ringed ones | Sibling icon buttons where some have a background class and some do not | Icon buttons in one row with and without a container | `unslop-surfaces` |
| Emoji as icons | Emoji in headings, buttons or list rows | Emoji code points in JSX strings | Emoji in text layers used as bullets or icons | `unslop-typography` |
| Sparkles | A sparkle or wand icon for anything described as smart | `Sparkles`, `Wand2`, `Zap` beside a label | The same icons | `unslop-surfaces` |
| Size soup | Five or more font sizes within a few pixels of each other | `text-xs`, `text-[13px]`, `text-sm`, `text-[15px]`, `text-base` in one view | More than five distinct sizes on one frame | `unslop-typography` |
| Mixed corner languages | Pills and circles beside rounded rectangles: a pill search bar over a rounded-rectangle bar, circular icon buttons beside rounded-square tiles | `rounded-full` and `rounded-xl` or `rounded-2xl` on sibling controls and containers | Fully round frames and partly rounded frames among the same kind of element | `unslop-surfaces` |
| Radius drift | 8, 10, 12, 16 and 20 all in use | More than three distinct `rounded-*` values in one view | More than three corner radius values on one frame | `unslop-surfaces` |
| Spacing drift | Gaps of 10, 12, 14, 16, 18 with no pattern | Arbitrary values such as `gap-[14px]`, `mt-[18px]` | Auto-layout gaps that are not on a 4px grid | `unslop-layout` |
| Title Case Everywhere | Every label capitalized like a headline | `Billing History`, `Start Sleep Tracking`, `Create New Project` | The same | `unslop-navigation`, as a `relabel` |
| Gradient text | A heading filled with the accent gradient | `bg-clip-text text-transparent bg-gradient-to-r` | A text layer with a gradient fill | `unslop-typography` |
| Pure black or white on color | `#000` or `#FFF` text and shadows over a tinted background | `text-white`, `#000000` shadows | `#FFFFFF` and `#000000` fills on a colored frame | `unslop-color` |

## Reading a screenshot only

With no source, the detection columns do not apply. Judge from the image and say every value is estimated:

- Sample the dominant background, the accent and the card fill. Name the hue family, not a hex.
- Count distinct text sizes and weights by eye.
- Count boxes: every shape with a visible edge or fill change.
- Name the kind of screen before judging density or scale.
- Run the squint and swap tests from the skill. They need nothing but the image.
