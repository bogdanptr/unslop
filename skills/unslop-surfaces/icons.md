# Icon sets

Where icons come from. An agent that draws icons from memory produces shapes that are slightly wrong, uneven in weight and different from one another, and that is one of the fastest ways a careful restyle still looks generated. Every icon in a result is a real file from one published set.

## Choose one set

Use the project's own set when it has one: an icon package in its dependencies, an icon component folder, or an icon library in the Figma file. Otherwise choose one of these and use it for every icon in the view.

| Set | Licence | Style | Filled variant | Reach for it when |
| --- | --- | --- | --- | --- |
| [Tabler Icons](https://github.com/tabler/tabler-icons) | MIT | Outline, 24 grid, 2px stroke, round joins | Yes, `filled` | The default choice. The largest set, so rare concepts are covered. Work views, tools, dashboards |
| [Lucide](https://github.com/lucide-icons/lucide) | ISC | Outline, 24 grid, 2px stroke, round joins | No | The project uses shadcn/ui or already has Lucide. Clean and neutral |
| [Heroicons](https://github.com/tailwindlabs/heroicons) | MIT | Outline at 1.5px, plus solid, at 24, 20 and 16 | Yes, `solid` | Tailwind projects, and anywhere a small exact set with matched solid versions is enough |
| [Phosphor](https://github.com/phosphor-icons/core) | MIT | Six weights: thin, light, regular, bold, fill, duotone | Yes, `fill` | Consumer and soft directions. The weights let icons match light or heavy type |
| [Material Symbols](https://github.com/google/material-design-icons) | Apache-2.0 | Outlined, rounded or sharp, variable weight | Yes, `-fill` | Android or Material products, and the widest coverage of all |
| [Iconoir](https://github.com/iconoir-icons/iconoir) | MIT | Outline, 24 grid, 1.5px stroke | No | Editorial and light directions that want a thinner line |

All six permit commercial use without visible attribution. Sets to avoid as a default: Feather, which is no longer maintained and is continued by Lucide, and any set whose licence asks for attribution or limits use, such as the free tiers of Font Awesome or Remix Icon, unless the project already uses it.

Never mix two sets in one view. A solid icon from one set beside an outline from another is the mixed-treatment tell.

## Get the real file

**In a project with a package manager**, install the set's package and import icons as components. Check the dependencies first and do not add a second set.

| Set | React | Vue | Plain SVG files |
| --- | --- | --- | --- |
| Tabler | `@tabler/icons-react` | `@tabler/icons-vue` | `@tabler/icons` |
| Lucide | `lucide-react` | `lucide-vue-next` | `lucide-static` |
| Heroicons | `@heroicons/react` | `@heroicons/vue` | `heroicons` |
| Phosphor | `@phosphor-icons/react` | `@phosphor-icons/vue` | `@phosphor-icons/core` |
| Material Symbols | `@material-symbols/svg-400` | the same | `@material-symbols/svg-400` |
| Iconoir | `iconoir-react` | `@iconoir/vue` | `iconoir` |

Adding a dependency is a change to the project. In `reskin` mode, or when editing production code in place, propose it in the report and use the set already present.

**In a single HTML file, or for Figma**, fetch each icon's SVG and place it inline. The files are served from the package on a public CDN:

| Set | Outline | Filled |
| --- | --- | --- |
| Tabler | `https://cdn.jsdelivr.net/npm/@tabler/icons@3/icons/outline/<name>.svg` | `…/icons/filled/<name>.svg` |
| Lucide | `https://cdn.jsdelivr.net/npm/lucide-static@1/icons/<name>.svg` | none |
| Heroicons | `https://cdn.jsdelivr.net/npm/heroicons@2/24/outline/<name>.svg` | `…/24/solid/<name>.svg` |
| Phosphor | `https://cdn.jsdelivr.net/npm/@phosphor-icons/core@2/assets/regular/<name>.svg` | `…/assets/fill/<name>-fill.svg` |
| Material Symbols | `https://cdn.jsdelivr.net/npm/@material-symbols/svg-400@latest/outlined/<name>.svg` | `…/outlined/<name>-fill.svg` |
| Iconoir | `https://cdn.jsdelivr.net/npm/iconoir@7/icons/regular/<name>.svg` | none |

Names are lowercase with hyphens, such as `truck`, `arrow-up-right`, `credit-card`. Material uses underscores, such as `local_shipping`. Check the major version in the URL against the package's current release before relying on it.

1. Fetch the file. A `404` means the name is wrong, not that the icon is missing: try the set's own name for the concept, such as `package` for a parcel or `building-store` for a shop.
2. Paste the `svg` element inline. Do not link to the CDN from the result, so the file works offline and does not depend on a third party.
3. Remove the fixed `width` and `height`, keep the `viewBox`, and size it with CSS.
4. Make sure color comes from `currentColor`. Outline sets already use it on `stroke`. For filled files set `fill="currentColor"`.
5. In Figma, insert the SVG as a vector node, name it `icon/<name>`, and bind its stroke or fill to the text color variable.

With no network access, say so, use the icons the source already has, and list the icons that still need replacing under **Not done**. Do not draw substitutes.

## Fit them to the type

- **Stroke weight** follows the text beside it. Tabler and Lucide ship at 2px: set `stroke-width="1.5"` beside regular text at 13 to 15px, and keep 2 beside medium or semibold. Phosphor uses a weight per file instead: `light` beside light text, `regular` beside regular, `bold` beside semibold.
- **Size** is 1 to 1.25 times the label's font size for inline icons, 20 to 24 in navigation and buttons, 16 in dense rows.
- **Outline is the default. Filled marks the active state**: the selected navigation item, a toggled control. Use the same icon's filled file, never a different icon. In a set with no filled variant, mark the active state with weight and color instead.
- **Keep the meaning.** Replace an emoji or a source icon with the set's icon for the same thing. A truck stays a truck.
- **One optical size per row.** Icons in the same row share a box size, so their labels line up.

## Report it

Name the set, its version and its licence in the report, under **Added**. When the icons were inlined, add a comment above the first one in the file with the set's name and licence.
