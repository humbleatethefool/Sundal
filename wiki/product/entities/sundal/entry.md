---
title: Entry
type: data-model-entity
template-version: 2
common-fields: []
sources: []
related: ["[[features/sundal/employee-app/purchase-log]]", "[[prds/sundal]]", "[[domain:entities/item]]", "[[domain:entities/purchase]]"]
created: 2026-11-23
updated: 2026-11-23
owner: product
authorship: curated
confidence: medium
instance-scope: user
---

## Definition

An entry is one snack line of a purchase: one item, the quantity taken and the price the employee saw. The Sundal module owns it, and each entry belongs to the employee whose purchase holds it. It is not a purchase ([[domain:entities/purchase]]), which holds one entry for each snack line, and it is not an item ([[domain:entities/item]]), which an entry takes.

## Data model

| Field | Type | Required | Searchable | References | Description | Example |
|---|---|:---:|:---:|---|---|---|
| purchase | ID | Y | N | — | The purchase that holds this entry. | `purchase_1042` |
| item | ID | Y | N | — | The snack the employee took. | `item_2007` |
| quantity | Integer | Y | N | — | How many of the item the employee took. | `2` |
| price | Money | Y | N | — | The price of one item, as shown when the purchase was made. | `20.00 INR` |

## Enumerations

None.

## Entries

None.

## Invariants

- An entry keeps the price it was made at, whatever the item's price becomes later ([[prds/sundal]]).
- An employee cannot cancel, edit or void an entry. Only the vendor can void one ([[prds/sundal]]; [[features/sundal/employee-app/purchase-log]] AC3).

## Lifecycle

An entry exists once its purchase is confirmed. The vendor can void it, which returns its quantity to stock ([[prds/sundal]]). The entity models no void state.

## Relationships

- Entry *—1 Purchase ([[domain:entities/purchase]]) — each entry belongs to one purchase, which holds one entry for each snack line.
- Entry *—1 Item ([[domain:entities/item]]) — each entry takes one item.
