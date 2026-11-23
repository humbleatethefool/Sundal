---
title: Cart
type: domain-object
template-version: 1
sources: []
related: []
created: 2026-11-17
updated: 2026-11-23
owner: domain
authorship: curated
confidence: medium
---

## Definition

A cart is the set of items a shopper has chosen and not yet bought. It is not a purchase, because nothing in it has been bought yet.

## Attributes

- shopper — person — the person this cart belongs to.
- lines — list — each line holds an item and the quantity chosen.
- total — money — the price of every line added together.

## Invariants

None.

## Lifecycle

A cart starts empty. It fills as the shopper adds items and changes quantities. It ends when the shopper buys it, which turns it into a purchase, or empties it.

## Related entities

- [[entities/item]] — what each line of the cart holds.
- [[entities/purchase]] — what a cart becomes when it is bought.
