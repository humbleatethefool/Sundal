---
title: Employee app
type: product-module
template-version: 1
sources: []
related: ["[[modules/sundal]]"]
depends-on: []
created: 2026-11-16
updated: 2026-11-16
owner: product
authorship: canonical
origination: originate
confidence: medium
audience: customer
kind: area
platforms: [mobile]
---


## Summary

The employee app is where an employee of a company the vendor serves records their own purchases at the shop. They add snacks to a purchase cart, review the total, and record it, and each snack line becomes its own entry. Employees cannot cancel an entry.


## Target users

- [[personas/employee]]: records their own purchases at the shop.


## Platform
 
Mobile only. Employees use it on a phone at the shop.


## Navigation

An employee signs in and lands on the home screen. The catalog lists the vendor's categories, and each category opens to its items. The cart is reached from the cart bar, and each recorded purchase has its own detail page.


## Features

- [[features/sundal/employee-app/record-a-purchase]] — an employee records what they took from the shop


## Entities
 
None.

## Quality attributes

- When the phone goes offline, a toast says "You're offline" and nothing else on screen changes.
- When an employee taps anything that needs the server while offline, the screen shows "You're offline" with a Retry button, and nothing changes on the server.
- An employee changes a quantity only with the + and − buttons, one step per tap, with no typing and no repeat on hold.


## Boundaries

None.


## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| What does the home screen show? | Shivani Erlewad | The employee app design starts |
| What sign-in method does an employee use? | Shivani Erlewad | The employee app design starts |
| How long is a saved cart kept? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |

