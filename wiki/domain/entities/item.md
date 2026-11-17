---
title: Item
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

An item is a snack the vendor sells, listed in a category. It has a name, an image, a description, a stock quantity and a price per item. It is not a purchase and not an entry, which record that an employee took it.

## Attributes

- name — text — what the item is called.
- image — image — a picture of the item.
- description — text — a short description of the item.
- stock quantity — whole number — how many of the item the vendor has.
- price per item — money — what one of the item costs.

## Invariants

None.

## Lifecycle

An item exists once the vendor adds it to a category. It is in stock while its stock quantity is above zero, and out of stock at zero. Its stock quantity goes down when a purchase of it is recorded and back up when an entry for it is voided.

## Related entities

- [[entities/category]] — the group that holds the item.
- [[entities/entry]] — one snack line of a purchase, which takes an item.
