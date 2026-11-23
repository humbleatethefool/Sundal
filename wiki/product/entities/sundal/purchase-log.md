---
title: Purchase log
type: data-model-entity
template-version: 2
common-fields: []
sources: []
related: ["[[features/sundal/employee-app/purchase-log]]", "[[domain:entities/purchase]]"]
created: 2026-11-23
updated: 2026-11-23
owner: product
authorship: curated
confidence: medium
instance-scope: user
---

## Definition

A purchase log is an employee's own list of every purchase they have recorded, from the first to the latest. The Sundal module owns it, and each purchase log belongs to one employee. It is not a purchase ([[domain:entities/purchase]]), and it holds nothing that a purchase does not already hold.

## Data model

| Field | Type | Required | Searchable | References | Description | Example |
|---|---|:---:|:---:|---|---|---|
| employee | ID | Y | N | — | The employee this purchase log belongs to. | `employee_318` |
| purchases | List<ID> | Y | N | — | Every purchase the employee has recorded. | `[purchase_1042, purchase_1043]` |

## Enumerations

None.

## Entries

None.

## Invariants

- A purchase log lists only its own employee's purchases ([[features/sundal/employee-app/purchase-log]] AC1).

## Lifecycle

A purchase log is empty until the employee records a purchase. It gains a purchase each time one is confirmed.

## Relationships

- Purchase log 1—* Purchase ([[domain:entities/purchase]]) — the purchase log lists every purchase its employee has recorded.
