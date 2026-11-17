---
title: Record a purchase
type: feature
template-version: 1
sources: []
related: ["[[modules/sundal/employee-app]]", "[[prds/sundal]]"]
depends-on: []
created: 2026-11-16
updated: 2026-11-16
owner: product
authorship: canonical
origination: originate
confidence: medium
---


## Summary

Record a purchase lets an employee add the snacks they took from the shop to a purchase cart, review the total, and record it. Each snack line becomes its own entry.


## Problem it solves

A snack shop vendor serving several companies is busy and has very little time to spare, so purchases often go unrecorded. Today one employee in each company records a whole day's purchases from everyone and gives the bill to the manager. With this feature, employees ([[personas/employee]]) record their own purchases on their phones, so the vendor has a record of every purchase without recording any of them.


## User story or flow

As an employee, I want to record the snacks I took from the shop on my phone, so that it's quick and no one has to record my purchases for me.


## Acceptance criteria

- **AC1.** A purchase exists only once the server has confirmed it.
- **AC2.** Retrying the same purchase never records it twice.
- **AC3.** Each snack line of a purchase is its own entry.
- **AC4.** Each entry keeps the price the employee saw when recording it.
- **AC5.** Recording a purchase takes its quantities out of stock.
- **AC6.** An item with none left shows "Out of stock".
- **AC7.** An employee cannot add more of an item than its stock allows, even when two employees buy the last one at the same moment.
- **AC8.** An employee never sees an item's stock number.
- **AC9.** Items in the cart stay on the employee's account until they record or remove them, including after signing out and back in.


## Quality attributes

None.

## Task flows

- [[flows/sundal/employee-app/record-a-purchase]] — an employee adds snacks to a purchase cart and records the purchase


## Surfaces

- **Categories** (list) — the vendor's categories, each opening to its items. States: loading, empty, error.
- **Category items** (list) — the items in one category, each with its image, name, description and price, and a way to add it to the cart. States: loading, empty, error.
- **Cart** (list) — the items the employee has added, with quantities, prices and the total, and the Record purchase action. States: loading, error.
- **Purchase detail** (detail) — one recorded purchase, with each line's item, quantity and price, the total and the time. States: loading, error.


## Success metrics & instrumentation

The release-level measure is that an employee records their everyday purchase easily. It is tracked in [[prds/sundal]].

These events instrument it:

- **Item added to cart** — an employee adds an item to the purchase cart.
- **Purchase recorded** — the server confirms a purchase.
- **Purchase recording failed** — the employee tries to record a purchase and the server does not confirm it.

These events show how many employees add items, how many of those purchases are recorded, and how many fail.


## Boundaries

- Paying for purchases, such as marking a month as paid, is V2 scope and not part of this feature.
- Walk-in cash sales happen outside the app and are not recorded here.


## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| What speed target defines "quick" for recording a purchase? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |

