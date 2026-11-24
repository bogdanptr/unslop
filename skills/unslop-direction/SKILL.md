---
name: unslop-direction
description: Picks the one visual idea a restyle is built on, for any kind of interface - dashboard, form, table, landing page, mobile screen, flow. Turns what the product is about into a short brief - atmosphere, signature, type voice, material and accent source - that every other unslop pass follows. Use before restyling a generic screen, when a design has no concept, or when asked for a visual direction, mood or art direction for an existing interface.
---

# Direction

This skill decides what the interface should feel like and why, before anything is restyled. It returns a brief short enough to hold in mind, and every later pass takes its decisions from it.

It decides and stops. `unslop-layout`, `unslop-dataviz`, `unslop-typography`, `unslop-color` and `unslop-surfaces` carry the brief out. The pipeline that calls this skill is `unslop`.

## One idea, taken from the product

A generic screen has no idea behind it, so each part falls back to a default. Giving it better defaults produces a more expensive-looking generic screen. What makes a design read as designed is that the parts agree with each other, and they agree because they come from one source.

That source is the product's own subject. A sleep app is about the night turning into morning. A billing tool is about money owed and money paid. A code review tool is about a diff. A reading app is about a page. When the background, the main element and the colors come from that subject, nobody needs to be told the screen was considered.

A direction that could be handed unchanged to a product in another category is not a direction. "Clean, modern, minimal" describes every screen that was ever sloppy.

How loud the idea is depends on the kind of screen. On most product interfaces it is quiet: a tinted neutral, one typeface with character, one accent with a reason. The idea still exists. It shows in a few exact decisions, not in a picture behind the content.

## 1. Say what the product is about

Write one line, in plain words, with a noun the user would recognize: *a night's sleep, from going to bed to waking up*, or *invoices: what is owed, by whom, since when*. Take it from the content contract, the product's own copy and its data, not from its category.

Then name the view's job as a question the user arrives with: *how did I sleep?*, *who has not paid?*, *is this plan right for my team?* Everything on the view supports that question or leaves.

## 2. Say what kind of screen it is

The kind sets how much expression the view can carry and where the idea can live. Name one:

| Kind | Examples | Time spent | Expression |
| --- | --- | --- | --- |
| **Focus** | A summary, a home screen, a detail view built around one figure or object | Seconds, often | High. The background and the main figure can both carry the idea |
| **Work** | Dashboards, tables, admin panels, editors, inboxes | Hours | Low. The idea lives in type, figures and the accent. The background is quiet |
| **Form** | Settings, checkout, sign-up, a composer | Minutes, with attention on input | Low. The idea lives in type, spacing and the controls |
| **Collection** | Feeds, galleries, search results, catalogs | Minutes, scanning | The content supplies the color. The interface steps back |
| **Marketing** | Landing pages, pricing, an empty-state or onboarding hero | Seconds, once | High. Large type, real product imagery, one strong composition |
| **Flow** | Onboarding steps, a wizard, a confirmation | Seconds per step | Medium. One thing per step. Consistency across steps matters most |
| **Overlay** | Dialogs, sheets, menus, popovers | Seconds | It takes the direction of the view behind it and adds nothing |

When a product has several kinds of screen, write one brief and say how each kind uses it: the marketing page at full strength, the dashboard at low strength, the same type and accent on both.

## 3. Find what is fixed

Check for a brand before choosing anything: documented colors, a typeface, a logo, a design-system file, tokens, a component library the project commits to. Fixed things stay fixed. A brand with a blue and a typeface still leaves atmosphere, signature and material open, and that is enough room.

A component library is a constraint, not a brand. Its default theme is exactly what the diagnosis flagged, so restyle through its tokens and keep its components.

When the source has no brand at all, which is usual for AI-generated screens, everything is open. Say so in the brief.

## 4. Choose where the look comes from

Pick the kind of thing the subject is. This decides what the look is made of:

| The subject is | The look comes from | Example products |
| --- | --- | --- |
| A time or a cycle | The sky or light at that time | Sleep, weather, calendars, habits |
| A place or a journey | Terrain, maps, horizon | Travel, running, delivery, logistics |
| A physical thing | Its material: paper, metal, card stock, fabric | Reading, notes, banking cards, audio gear, tickets |
| An instrument or a measure | Dials, grids, precision, mono type | Finance, analytics, monitoring, developer tools |
| A document or a record | The printed form: ledgers, receipts, forms, statements | Invoicing, accounting, legal, health records, HR |
| Content made by people | The content itself: photos, covers, text | Social, media, commerce |
| A conversation | The exchange: turns, voices, a thread | Chat, support, assistants, email |
| A state of mind | Light and softness, or their absence | Meditation, focus, journaling |

The starting archetypes for each, with their dials already set, are in [directions.md](directions.md). Use one as a starting point and change at least one dial so it fits this product. An archetype applied unchanged is a template again.

## 5. Set five dials

Each dial is one decision. Make all five. A dial left open gets filled with a default by whichever pass meets it first.

| Dial | Decide | Owner of the execution |
| --- | --- | --- |
| **Atmosphere** | What the background is and what it stands for. A deliberate quiet neutral on work, form and collection screens. A gradient of a real phenomenon, a material or an image where the kind allows it | `unslop-color` |
| **Signature** | The one element that carries the idea, and its form. See below | `unslop-dataviz` for a figure or chart, `unslop-typography` for type, `unslop-layout` for a composition |
| **Type voice** | The character of the typeface and how heavy the large text is | `unslop-typography` |
| **Material** | What surfaces are made of: flat, matte, paper, glass | `unslop-surfaces` |
| **Accent source** | Where the one accent color comes from: a stop of the atmosphere, the brand, the content, a color the subject already has | `unslop-color` |

The signature is the thing a viewer would describe afterwards. One per product, and it depends on the kind of screen:

| Kind | Where the signature usually is |
| --- | --- |
| Focus | The form of the main figure: an arc for a night, a route line for a run, a card for an account |
| Work | How figures and tables are set: a mono for numbers, a distinctive table rhythm, one chart style used everywhere |
| Form | The controls and the type: a field style, a section rhythm, a heading face |
| Collection | The item: its crop, its caption style, its hover or selected state |
| Marketing | The headline treatment and the product shown for real, not as an illustration of it |
| Flow | A progress device or a recurring composition that every step shares |

The dials must agree. A warm dawn atmosphere with a cold blue accent and a brutalist mono typeface is three ideas.

Quiet is a valid setting for every dial, and the right one more often than not. Do not put a sunset behind a spreadsheet, a glass card over a settings form or an illustration on a table.

## Quiet is not timid

The kind of screen sets a ceiling on expression. On focus, marketing and flow views it also sets a floor. A restyle that only tidies such a view, with better spacing, fewer borders and a calmer palette, is a cleaner version of the generic screen and not a design.

On those kinds, one object carries the idea at full strength and everything around it stays quiet:

- **Choose the object.** It is the focal point `unslop-layout` names: the main figure, the headline block, the item being shown.
- **Give it the brand or accent color as a field**, not as a trim. A balance on a card in the brand color, a headline on a full-bleed block. The page around it stays neutral. How color behaves on a field belongs to `unslop-color`.
- **Give it something from the subject**: a form, a texture or a material that this product has and another would not. Engraved line work for money, contour lines for terrain, a ruled grid for an instrument, a paper edge for a document. The recipe is in `unslop-surfaces`.
- **Set its largest text in the display face** when the brief has one.

Strength is concentrated, never spread. One object at full strength reads as confident. Three at medium strength read as busy.

Write it in the brief as one more line: `Strength: the balance card. Brand blue field, engraved rosette, serif figures. Everything else on paper.` On work, form and collection views the line is `Strength: none. The idea is in the type and the figures.`

## 6. Write the brief

```markdown
## Direction: <product>, <view>

About: invoices: what is owed, by whom, since when
The view's job: who has not paid?
Kind: work
Fixed: nothing documented

Atmosphere: warm paper white, flat. The page is a ledger, not a dashboard
Signature: amounts set in a mono with tabular figures, right-aligned, overdue ones carrying the accent
Type voice: a grotesque for interface text, its matching mono for every figure
Material: paper. Hairline rules between rows, no cards
Accent source: the red of an overdue stamp, used only on overdue amounts and the one primary action

Avoid: stat cards with tinted icon tiles, indigo accent on gray-50, a card around every section
```

The same structure on a focus screen:

```markdown
About: a night's sleep, from going to bed to waking up
The view's job: how did I sleep?
Kind: focus
Fixed: nothing documented

Atmosphere: the sky before sunrise, cool at the top warming to the horizon. It is the morning the user wakes into
Signature: an arc from bedtime to wake time, moon at one end, sun at the other, duration at its center
Type voice: soft geometric sans, large figures at light weight
Material: glass over the sky, one level, no borders
Accent source: the warmest stop of the sunrise, used on the one primary action

Avoid: a ring around the score, an indigo accent on navy, tinted icon tiles
```

Every line is a decision someone could check a screen against. Close with the three tier 1 tells from the diagnosis as an **Avoid** line, so no pass drifts back to them. Name the default, not the raw property: `indigo accent on navy`, not `indigo`. A bare hue in the Avoid line will collide with an atmosphere that legitimately contains it.

For several screens, write one brief. The atmosphere may shift between screens when the shift means something. The type, the material and the accent rule stay the same.

## Before you finish

| You notice | Fix |
| --- | --- |
| The brief would fit a product in another category | Go back to **Say what the product is about** and name its subject |
| No `Kind:` line in the brief | Name the kind. It sets how loud every dial may be |
| "Clean", "modern", "minimal", "premium" or "sleek" in the brief | Replace each with the decision it was standing in for |
| An atmosphere chosen because it looks good, with no link to the subject | Say what it stands for, or choose a quiet neutral |
| A gradient or image atmosphere on a work, form or collection screen | A quiet tinted neutral. Put the idea in the signature and the type |
| A focus, marketing or flow view with no `Strength:` line, or with nothing at full strength | Choose the focal object and give it the field, the subject's detail and the display face |
| Full strength on more than one object in a view | Keep it on the focal object and quiet the rest |
| A brand color that exists and appears only as small trim on a focus view | Use it as a field on the focal object |
| Glass as the material on a screen with a flat background | Flat, matte or paper |
| A signature that is a chart, on a view with no figure worth a chart | Move the signature to type, controls or composition |
| A dial left as "to be decided" or "depends" | Decide it |
| The brief overrides a documented brand color or typeface | Restore the brand and move the idea to the open dials |
| More than one accent hue | Keep one. Status colors are not accents and belong to `unslop-color` |
| Two briefs for two screens of one product | Merge them. Only the atmosphere and the strength may vary, and only with a reason |
