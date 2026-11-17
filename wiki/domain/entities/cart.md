---
title: Cart
type: domain-object
template-version: 1
sources: []
related: []
created: 2026-11-17
updated: 2026-11-17
owner: domain
authorship: curated
confidence: medium
---

## Definition

A cart is the set of items an employee has added to a purchase and not yet recorded. It belongs to one employee and is kept on their account. It is not a purchase, because nothing in it has been recorded or taken out of stock.

## Attributes

- employee — person — the employee this cart belongs to.
- lines — list — each line holds an item and the quantity the employee has added.
- total — money — the price of every line added together.

## Invariants

None.

## Lifecycle

A cart starts empty. It fills as the employee adds items and changes quantities. It ends when the employee records it, which turns it into a purchase, or empties it.

## Related entities

- [[entities/item]] — what each line of the cart holds.
- [[entities/purchase]] — what a cart becomes when it is recorded.
