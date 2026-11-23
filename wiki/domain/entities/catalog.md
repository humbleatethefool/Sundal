---
title: Catalog
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

A catalog is everything a shop offers for sale, grouped into categories. Shoppers look through it to choose what to buy. It is not a cart, which holds only what a shopper has chosen.

## Attributes

- categories — list — the groups the shop's items are sorted into, each holding its items.

## Invariants

None.

## Lifecycle

A catalog changes as the shop adds or removes categories and items.

## Related entities

- [[entities/category]] — a group within the catalog.
- [[entities/item]] — a snack the catalog offers.
