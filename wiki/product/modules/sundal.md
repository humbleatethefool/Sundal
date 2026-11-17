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

Sundal is a mobile app that helps a snack shop vendor manage stock and see how much each company owes for the snacks its employees took that month. Employees of the companies record their own purchases at the shop, and the vendor sees what each company's employees bought and each company's monthly total. Company admins see only their company's monthly total.


## Target users

- Vendor: runs the shop and manages stock, prices and what each company owes.
- [[personas/employee]]: records their own purchases at the shop.
- Company admin: sees the company's monthly total.


## Platform

Mobile only, for vendors, employees and company admins.


## Navigation

Each person sees only the area for their role: employees record purchases, vendors manage the shop, and company admins see only their company's monthly total. The employee area is described on [[modules/sundal/employee-app]].


## Features

None.


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
| What measurable target defines "simple for non-technical users and light on data"? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| What does the home screen show for each role? | Shivani Erlewad | The employee app design starts |
| In what order do the vendor app and company access follow the employee app? | Shivani Erlewad | The employee app design is complete |
| Who adds companies and employees to Sundal, and how do employees get their sign-in? | Shivani Erlewad | The employee app design starts |


