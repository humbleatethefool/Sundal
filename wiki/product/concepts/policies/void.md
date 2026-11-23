---
title: Void
type: concept
template-version: 1
sources: []
related: []
created: 2026-11-23
updated: 2026-11-23
owner: product
authorship: curated
confidence: medium
---

## Definition

To void an entry is to remove one snack line of a purchase, which only the vendor can do. Voiding returns the entry's quantity to stock. An employee cannot cancel, edit or void an entry. A void of an entry in a closed month leaves that month unchanged and appears in the open month as a labeled line.

## Usage

The vendor voids one entry at a time, and the rest of the purchase stays as it was. An employee who recorded a wrong line cannot undo it, so the line stays until the vendor voids it. How a voided entry is stored or shown is undecided, and [[entities/sundal/entry]] models no void state.

> [!warning]
> A void is not a stock edit. The vendor changes stock counts directly in a separate action. A void returns stock only as a result of removing an entry.

## Examples

- An employee records 2 packets of chips and a drink, and the chips line was a mistake. The vendor voids the chips entry. The 2 packets return to the item's stock, and the drink entry stays.
- An entry from last month is voided this month. Last month's total does not change. This month shows a labeled line for the void.

## Non-examples

- An employee cancelling an entry. The employee has no way to do this.
- The vendor changing an item's stock count directly. That is a stock edit.

## Boundaries

None.

## Related concepts

- [[entities/sundal/entry]] — the entity a void acts on.
- [[domain:concepts/stock]] — where the voided quantity returns.
