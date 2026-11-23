---
title: Sundal
type: product-module
template-version: 1
sources: []
related: ["[[prds/sundal]]"]
depends-on: []
created: 2026-11-16
updated: 2026-11-16
owner: product
authorship: canonical
origination: originate
confidence: medium
audience: customer
kind: application
platforms: [mobile]
---

## Summary

Sundal is a snack shop product with a separate mobile app for each of its users: employees, vendors and company admins.


## Target users

- Vendor: runs the shop and manages stock, prices and what each company owes.
- [[personas/employee]]: records their own purchases.
- Company admin: sees the company's monthly total.


## Platform

Mobile only, for vendors, employees and company admins.


## Navigation

Each person sees only the area for their role: employees record purchases, vendors manage the shop, and company admins see only their company's monthly total. The employee area is described on [[modules/sundal/employee-app]].


## Features

- [[features/sundal/employee-app/sign-in]] — an employee signs in with their mobile number and a one-time code
- [[features/sundal/employee-app/record-a-purchase]] — an employee records what they took from the shop
- [[features/sundal/employee-app/purchase-log]] — an employee looks through the purchases they recorded and checks one


## Entities

None.


## Quality attributes

- Every screen needs an internet connection. The app does not work offline.
- All text in the app is in English.


## Boundaries

None.


## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Who adds companies and employees to Sundal? | Shivani Erlewad | The employee app design starts |

