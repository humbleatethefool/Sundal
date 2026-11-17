---
title: Purchase
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

A purchase is a record that an employee took snacks from the shop, made when the server confirms a recorded cart. It holds one entry for each snack line. It is not a cart, which has not been recorded yet.

## Attributes

- employee — person — the employee who made this purchase.
- entries — list — one entry for each snack line.
- total — money — the price of every entry added together, at the prices the employee saw.
- time — date and time — when the purchase was recorded.

## Invariants

None.

## Lifecycle

A purchase exists only once the server has confirmed it. Recording the same cart again never makes a second purchase. After that, the employee cannot cancel its entries. The vendor can void one entry of it.

## Related entities

- [[entities/cart]] — what a purchase comes from.
- [[entities/entry]] — one snack line of the purchase.
