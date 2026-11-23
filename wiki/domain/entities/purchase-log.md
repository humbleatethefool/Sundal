---
title: Purchase log
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

A purchase log is a shopper's own list of the purchases they have made, from the first to the latest. It is not a purchase, and it holds nothing that a purchase does not already hold.

## Attributes

- shopper — person — the person this purchase log belongs to.
- purchases — list — every purchase the shopper has made.

## Invariants

None.

## Lifecycle

A purchase log is empty until the shopper makes a purchase. It gains a purchase each time one is made.

## Related entities

- [[entities/purchase]] — what the purchase log lists.
