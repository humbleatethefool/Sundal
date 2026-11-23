---
title: Purchase
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

A purchase is a record that a shopper bought items from a shop. It holds one entry for each line of items. It is not a cart, which has not been bought yet.

## Attributes

- shopper — person — the person who made this purchase.
- entries — list — one entry for each line of items.
- total — money — the price of every entry added together, at the prices shown at the time.
- time — date and time — when the purchase was made.

## Invariants

None.

## Lifecycle

A purchase exists once the shopper has bought the items. It is a record of what was bought and at what price.

## Related entities

- [[entities/cart]] — what a purchase comes from.
