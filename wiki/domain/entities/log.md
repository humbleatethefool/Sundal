---
title: Log
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

A log is an employee's own list of every purchase they have recorded, from the first to the latest. It shows only that employee's purchases. It is not a purchase, and it holds nothing that a purchase does not already hold.

## Attributes

- employee — person — the employee this log belongs to. It lists only that employee's purchases.
- purchases — list — every purchase the employee has recorded.

## Invariants

None.

## Lifecycle

A log is empty until the employee records a purchase. It gains a purchase each time one is confirmed.

## Related entities

- [[entities/purchase]] — what the log lists.
