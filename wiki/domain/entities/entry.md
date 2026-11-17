---
title: Entry
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

An entry is one snack line of a purchase: one item, the quantity taken and the price the employee saw. The vendor can void one entry. It is not a purchase, which holds one entry for each snack line.

## Attributes

- item — item — the snack the employee took.
- quantity — whole number — how many of the item were taken.
- price — money — the price per item shown when the purchase was made.

## Invariants

None.

## Lifecycle

An entry exists once its purchase is confirmed. It keeps the price it was made at. The vendor can void it, which returns its quantity to stock. An employee cannot cancel it.

## Related entities

- [[entities/purchase]] — the purchase that holds the entry.
- [[entities/item]] — what the entry took.
