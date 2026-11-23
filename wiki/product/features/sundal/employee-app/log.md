---
title: Log
type: feature
template-version: 1
sources: []
related: ["[[modules/sundal/employee-app]]", "[[prds/sundal]]", "[[features/sundal/employee-app/record-a-purchase]]"]
depends-on: ["[[features/sundal/employee-app/record-a-purchase]]"]
created: 2026-11-23
updated: 2026-11-23
owner: product
authorship: canonical
origination: originate
confidence: low
---


## Summary

Log lets an employee look through the purchases they recorded and open one to check what it holds.


## Problem it solves

An employee ([[personas/employee]]) records purchases on their own phone and may later want to check one: what they took, at what price and when. Without a way back to a recorded purchase, the employee cannot confirm a line was right.


## User story or flow

As an employee, I want to find a purchase I recorded earlier, so that I can check what it holds.


## Acceptance criteria

- **AC1.** The list and every purchase in it belong to the signed-in employee. No other employee's purchase is ever shown.
- **AC2.** A line shows the price the employee saw when recording, even if the item's price has changed since.
- **AC3.** No screen in this feature offers the employee a way to cancel, edit or void an entry.


## Quality attributes

None.


## Task flows

- [[flows/sundal/employee-app/log]] — an employee finds a purchase they recorded earlier and checks what it holds


## Surfaces

- **Log** (list) — the employee's recorded purchases, each opening that purchase. States: loading, empty, error.


## Success metrics & instrumentation

None.


## Boundaries

- Recording a purchase is not part of this feature. See [[features/sundal/employee-app/record-a-purchase]].
- The employee cannot cancel, edit or void an entry. Only the vendor voids an entry.
- The Purchase detail screen is also reached right after a purchase is recorded. That arrival belongs to [[features/sundal/employee-app/record-a-purchase]].


## Open questions

- Which feature lists the Purchase detail surface? Record a purchase lists it, and this feature opens it too. Owner: Shivani Erlewad. Resume when the feature pages are reviewed together.
- In what order does the list show purchases, and how does a purchase with a voided entry show? The Entry entity has no void state yet. Owner: Shivani Erlewad. Resume when the vendor's void screens are designed.
