---
name: unslop-navigation
description: Simplifies navigation and interface labels on a generic interface - tab bars, sidebars, top navigation, page headers, breadcrumbs, in-page tabs and button labels. Reduces the number of destinations, gives them names that say what is there, shortens labels and restyles the navigation to match the screen. Use when a nav has too many vague items, labels are wordy or in title case, a header repeats what is obvious, or as the navigation pass of unslop.
---

# Navigation and labels

This skill makes the routes out of a view fewer and clearer: how many destinations, what they are called, what the header carries and what buttons say. It also restyles the navigation so it belongs to the rest of the screen.

Every destination still has to be reachable afterwards. What may be removed or merged, and how that is recorded, belongs to `unslop`'s content contract. Icon style and the navigation's material belong to `unslop-surfaces`. Colors belong to `unslop-color`. Type sizes belong to `unslop-typography`.

## Labels may change, destinations may not

Wording is a judgment: pick the plainest word a user would say. Reachability is not: after this pass, every route, handler and destination in the contract is still reachable, and the ledger says how.

Interface labels are open to rewording. Data, user content and anything the product's voice guide fixes are not.

In `reskin` mode, change nothing structural: the same items with the same names and the same button labels. Apply only the styling rules. In code, removing or merging a destination changes routing, so propose it in the report and apply it only when the user asked for a rework or approves.

A view with no navigation of its own, such as a dialog or a single landing page, skips the structural rules. The label rules still apply.

## Fewer destinations

A generated navigation has as many items as fit. Each item is a promise that the user needs that place often.

| Pattern | Target | Past that |
| --- | --- | --- |
| Tab bar on a phone | 3 or 4. Five only when each is used daily | Demote the least used behind an avatar or a "More" destination |
| Sidebar | 5 to 7 top-level items, in at most 3 groups | Group, collapse the rarely used group, or move settings-like items to the account menu |
| Top navigation | 4 to 6 links and one action | Fold the rest into one menu |
| In-page tabs | 2 to 5 | A select, or split the page |
| Breadcrumbs | Only where the hierarchy is three levels or deeper | Remove them on a two-level product. The back control is enough |

- An item earns its place when it is a top-level place the user goes to **directly and often**. Count how the product's own content refers to it.
- **Merge** two items that show the same kind of thing at different depths, such as a summary and its history, or `Analytics` and `Reports`.
- **Demote** an item that is a feature of another place, or one that is used rarely. Its entry point moves into the view it belongs to, or into the account menu.
- **Account, profile and settings** share one destination.
- **Two navigations for the same level** is one too many. A sidebar and a top bar that both list sections: keep one for sections, give the other to context such as the workspace, search and the account.

For every item removed, write the ledger row: what it was, where its entry point now lives. If you cannot name the new entry point, the item stays.

The new entry point has to be on a view in scope, where it can be built and checked. When the only home for an item is a view outside this run, keep the item and list the removal under **Proposed, not applied**.

## Names that say what is there

- **One or two words**, a noun the user would say aloud.
- **Name the content, not the container.** `Today`, `Invoices`, `Inbox` say what is there. `Home`, `Dashboard` and `Overview` say only that it is first.
- **No pairs that overlap.** `Stats` beside `Insights`, `Profile` beside `Account`, `Settings` beside `Preferences` each force a guess.
- **Sentence case**, set as text and not with an uppercase transform. This applies to every interface label, not only navigation: `Deep Sleep` becomes `Deep sleep`, `Billing History` becomes `Billing history`. Each change is a `relabel` in the ledger. Skip it in `reskin` mode and for product names.
- **Keep product nouns.** If the product calls it a Journal or a Workspace everywhere, that is its name.

Record every rename as `relabel` with the old name. A renamed item opens the same route.

## The current place is marked, quietly

- Every item shows a label. Icon-only navigation saves a few pixels and costs comprehension. An icon-only collapsed sidebar is fine when it expands and each icon has a tooltip.
- The selected item is marked by full-strength text and, where there are icons, a filled variant. Inactive items sit at about 55 to 65 percent.
- A capsule behind the selected item is a good third signal when it is quiet: the accent at 8 to 10 percent over the bar's surface, or one fill step, covering the icon and the label together, with the bar's radius minus its padding. The icon and label inside may take the accent. A saturated accent pill behind the icon alone, a glow, or accent color with no change of shape is not.
- One icon set, the same one the rest of the interface uses. In a sidebar, drop the icons entirely when the labels are clear and the list is short. A column of twelve icons nobody can tell apart is decoration.
- Counts and badges appear only where a number is waiting for the user. A badge on every item is noise.

## The navigation belongs to the screen

- It takes the screen's material from the brief. On a flat or paper direction a sidebar is the page color or one fill step from it, separated by space or one hairline, not a dark slab beside a light page unless the brand is built on that.
- A floating bar on a phone is inset 12 to 16 from the screen edges with the card radius or larger. A docked bar spans the width and respects the bottom safe area.
- Content scrolls beneath fixed navigation, and the last item of the content can be scrolled fully clear of it.
- A persistent search or assistant field is not part of the navigation. It gets its own surface, and when the product leads with it, more visual weight than the navigation. How two floating bars stay distinct belongs to `unslop-surfaces`.
- A sidebar is 220 to 280 wide. Its items are 32 to 40 tall on desktop, with the label on the same baseline as its icon.
- Its hairline or shadow follows `unslop-surfaces`.

## Headers carry context, not titles

- Remove a header title that repeats the selected navigation item or the view's obvious subject. Keep it when it is the only place the view is named.
- Keep what orients and scopes: a date range, a filter, a back control, the workspace, the account.
- A greeting is not a header. Its size is `unslop-layout`'s call.
- One row. Title or context leading, actions trailing. On desktop the page's primary action sits here.
- A marketing header is the logo, four to six links and one action. The action is the only filled element.

## Buttons say the action in as few words as it takes

- A verb, one or two words. `Start`, `Save`, `Add entry`, `Send invoice`.
- Drop words the view already supplies. On a sleep screen with one action, `Start Sleep Tracking` is `Start`. On an invoice, `Send This Invoice Now` is `Send`.
- A shortened label must still make sense where the button sits. `Start` alone in a toolbar with five other controls is not clear.
- Keep the full phrase when the short one is ambiguous, when two actions sit together or when the action is destructive. `Delete` beside `Delete account` is not a saving.
- The accessible name stays specific. A button that shows `Start` keeps an accessible label such as `Start sleep tracking`.
- Marketing actions name what happens next: `Start free trial`, `Book a demo`. `Get started` and `Learn more` say nothing.
- Links such as `View all` become the destination's name, once per view at most.

Record each rewording as `relabel`. Never reword data, legal text, user content or strings the brand voice documents.

## Before you finish

| You notice | Fix |
| --- | --- |
| A destination removed with no ledger row naming its new entry point | Add the entry point and the row, or restore the item |
| A route, link or handler from the contract that nothing on the result reaches | Restore the way to it |
| Items removed or renamed in `reskin` mode | Restore them |
| A destination removed in code without it being proposed or requested | Revert the routing change and list it under **Proposed, not applied** |
| A first item called `Home`, `Dashboard` or `Overview` | Name what it shows |
| Two items with overlapping names | Merge them or rename one |
| A sidebar with more than seven ungrouped items | Group, collapse or demote |
| A sidebar and a top bar listing the same sections | One lists sections, the other carries context |
| Breadcrumbs on a two-level product | Remove them |
| An item with an icon and no label, and no tooltip | Add the label |
| The selected item marked only by color | Add full-strength text and the filled icon variant or a quiet fill |
| A saturated accent pill or glow behind the selected icon | A quiet tinted capsule around icon and label, or none |
| A search or assistant field that reads as part of the navigation bar | Its own surface, in a different tone |
| A notification badge on most navigation items | Keep the ones with something waiting |
| Navigation in a material the rest of the screen does not use | Give it the screen's material |
| A header title identical to the selected item's label | Remove the title |
| A button label of three or more words where one is unambiguous | Shorten it and keep the full accessible name |
| `Get started` or `Learn more` as a call to action | Name what happens next |
| A shortened label on a destructive or ambiguous action | Restore the specific wording |
| A data value or user string reworded | Restore it from the contract |
