---
title: Category
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

A category is a named group of items in a snack shop's catalog, which the vendor creates and names. It holds items directly. It is not a subcategory, and it is not an item.

## Attributes

- name — text — what the vendor calls the category. It is the name shown on the categories list.

## Invariants

None.

## Lifecycle

A category exists once the vendor creates and names it. It then holds the items the vendor adds to it.

## Related entities

- [[entities/item]] — what a category holds.
