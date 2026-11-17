---
title: Catalog
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

A catalog is everything a vendor offers in the shop: the categories the vendor creates and the items in them. The vendor builds it, and employees look through it to choose what they take. It is not a cart, which holds only what an employee has chosen.

## Attributes

- categories — list — the vendor's categories, each holding its items.

## Invariants

None.

## Lifecycle

A catalog grows as the vendor creates categories and adds items to them.

## Related entities

- [[entities/category]] — a group within the catalog.
- [[entities/item]] — a snack the catalog offers.
