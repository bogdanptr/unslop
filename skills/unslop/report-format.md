# Report format

What the user reads after the work. Lead with where the result is, then why it looks the way it does.

```markdown
## Unslopped: <screen name>

**Mode** full · **Source** <frame link or path> · **Result** <copy frame link, branch or URL>

**Direction** <one sentence: what the product is about and the idea that follows from it>

### What changed

| Before | After | Why |
| --- | --- | --- |
| Four stat cards, two charts and a table at equal weight | Outstanding total leads, the invoice table directly under it | The view answers one question: who has not paid |
| Donut of invoice statuses with a legend | One segmented bar, labeled directly | Three parts of one whole do not need a legend |
| Indigo accent on gray-50, white bordered cards | Warm paper page, hairline rules, red only on overdue amounts | The accent now means overdue and nothing else |
| Icons in tinted square tiles beside every stat | Label and value pairs in the page header | Fewer boxes, the figures read first |
| Sidebar of 11 items, first one `Dashboard` | 6 items in 2 groups, first one `Invoices` | Fewer destinations, names that say what is there |

### Content ledger

| ID | Element | Disposition | Where it is now |
| --- | --- | --- | --- |
| ... | ... | ... | ... |

**Needs data.** `invoice.dueDate` for 3 rows: the due column shows a marked placeholder.
**Assumed.** The Reports view holds the revenue chart (the source links to it with `View all`; not visible in a screenshot).
**Proposed, not applied.** Merging `Analytics` into `Reports` in the sidebar (code change to navigation).
**Not done.** <passes skipped and why>
**Not verified.** <checks that could not be run>
```

## Rules

- One row per decision in **What changed**, most visible first, 5 to 10 rows. Not one row per CSS property.
- The **Why** cell names the reason in the product's terms. "More modern" and "cleaner" are not reasons.
- The ledger is complete. Every contract row appears once.
- Omit a closing line that has nothing in it.
- No adjectives about the result. The user is looking at it.
- For several screens, one report: the direction once, then a short table per screen and one merged ledger.
