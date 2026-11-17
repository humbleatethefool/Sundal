---
title: Sundal
type: prd
template-version: 1
status: draft
sources: []
related: []
created: 2026-11-16
updated: 2026-11-16
owner: product
authorship: canonical
origination: originate
confidence: medium
---

## Problem statement

A snack shop vendor serves the employees of several companies. The vendor is busy making tea and doing other work, so purchases often go unrecorded, and even with time to spare they prefer not to record them. Instead, the vendor relies on each company to record its bill and pay every month.

- **Vendor:** has no record of their own, so they trust each company's bill. They still need to keep stock counts, know what each company's employees took, and work out what each company owes.
- **Employee:** one employee in each company records a whole day's purchases from everyone, and not only their own.
- **Company admin:** receives that bill from the employee and pays the vendor every month.


## Metadata

- Author: Shivani Erlewad
- Target release: Employee mobile app first. Vendor and company mobile app follow, with no dates set.
- Core team: Shivani Erlewad, UX designer (sole team member).


## Why now / evidence

None yet.


## Objective & goals

Give the vendor a fast way to manage stock and see what each company owes. Let employees record their own purchases on their phones, so the vendor has a record without recording anything. Let each company see the monthly amount it owes, as a cumulative total.


## Target audience / users

- Vendor: runs the shop from a phone and has very little time to spare. Serves several companies, sets prices and stock, and can void one entry.
- Employee: works at a company the vendor serves. Uses a phone at the shop, has one personal sign-in on one phone at a time, and records only their own purchases.
- Company admin: uses a phone. Sees the company's monthly total only, never who bought what.


## Success metrics

For the first release, an employee can record their everyday purchase easily. The measure of "easily" is not yet set.


## Assumptions

- Vendors keep stock counts accurate by updating them themselves. Walk-in cash sales happen outside the app and are not recorded, so counts can drift from the shelf.
- Employees take only what they record, and record their own purchases at the shop.
- Vendors, employees and company admins all have a phone with an internet connection. The app works only online.
- A company admin needs only a monthly total. They don't need to see who bought what.


## Requirements / solution

### Functional

| Requirement | Priority |
|---|---|
| As an employee, I record my own purchases at the shop from my phone. | Must |
| As a vendor, I set prices and manage stock from my phone. | Must |
| As a vendor, I see what each company's employees have bought and the monthly total each company owes. | Must |
| As a vendor, I void one entry. | Must |
| As a company admin, I see my company's monthly total from my phone. | Must |
| A purchase keeps the price shown when it was made. | Must |

### Non-functional

| Requirement | Priority |
|---|---|
| English only, built for all of India. | Must |
| Phones only, for vendors, employees and company admins. | Must |
| Online only: a purchase exists only once the server confirms it, and retrying never records it twice. | Must |
| Light on data, simple for non-technical users. | Should |


## Out of scope

- Payment features (V2): marking a month as paid, the vendor raising an invoice, and the company paying in the app.
- Recording walk-in cash sales, which happen outside the app.
- Offline use. Every screen needs an internet connection.
- Languages other than English.
- Subcategories. A category holds items directly.
- Choosing the technology. This work covers UX screens only.


## Dependencies & risks

- Dependencies: None. One person, a UX designer, is working on Sundal.
- Risk: stock counts can drift from the shelf, because walk-in cash sales are not recorded. Mitigation: only the vendor changes stock counts directly.
- Risk: the vendor has very little time, so a slow or complex screen may go unused. Mitigation: keep each screen simple and check it in testing.


## Timeline / milestones

- First: the employee mobile app.
- Then: the vendor app and company access.
- No dates are set.


## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| What evidence shows this problem is worth solving now? | Shivani Erlewad | A vendor conversation or shop visit is done |
| How will "records a purchase with ease" be measured, and what number counts as success? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| In what order do the vendor app and company access follow the employee app? | Shivani Erlewad | The employee app design is complete |
| How will the company pay in V2? | Shivani Erlewad | V2 scope is taken up |
| Who adds companies and employees to Sundal? | Shivani Erlewad | The employee app design starts |


## Supporting documentation

None
