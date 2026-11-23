---
title: Entry
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

An entry is one line of a purchase: one item, the quantity bought and the price at the time. It is not a purchase, which holds one entry for each line.

## Attributes

- item — item — the snack bought.
- quantity — whole number — how many units of the item were bought.
- price — money — the price per unit shown when the purchase was made.

## Invariants

None.

## Lifecycle

An entry exists once its purchase exists. It keeps the price it was made at.

## Related entities

- [[entities/item]] — what the entry took.
- [[entities/purchase]] — the purchase that holds the entry.
