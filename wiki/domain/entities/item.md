---
title: Item
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

An item is a snack a shop sells, listed in a category. It has a name, an image, a description, a price per item and a stock quantity. It is not a purchase and not an entry, which record that someone bought it.

## Attributes

- name — text — what the item is called.
- image — image — a picture of the item.
- description — text — a short description of the item.
- stock quantity — whole number — how many units of the item the shop has.
- price per item — money — what one unit of the item costs.

## Invariants

None.

## Lifecycle

An item exists once the shop lists it. It is in stock while its stock quantity is above zero, and out of stock at zero. Its stock quantity goes down as units are sold and up when the shop restocks.

## Related entities

- [[entities/category]] — the group that holds the item.
