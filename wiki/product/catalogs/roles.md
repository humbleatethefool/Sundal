---
title: Roles
type: catalog
template-version: 1
sources: []
related: []
created: 2026-11-17
updated: 2026-11-17
owner: product
authorship: curated
confidence: medium
---

## Purpose

The roles catalog lists the people who use Sundal and the role each one holds. The product owner governs membership. Product pages, screens and the design wiki's sitemaps resolve a role name against this list.

## Entries

| Code | Meaning | Governed by | Notes |
|---|---|---|---|
| `vendor` | Runs the snack shop and serves several companies. Sets prices and stock, sees what each company's employees bought and what each company owes, and can void one entry. | product | Uses a phone. |
| `employee` | Works at a company the vendor serves. Records their own purchases at the shop. Cannot cancel an entry. | product | Uses a phone. Signs in with their mobile number. One sign-in, active on one phone at a time. |
| `company-admin` | Works at a company the vendor serves. Sees the company's monthly total, never who bought what. Fills in the details of the company's employees. | product | Uses a phone. |

## Governance

None.

## Boundaries

- What each role may do on each screen is not listed here. That belongs to an access model, which the wiki does not have yet.

## Consumers

- [[modules/sundal]] — names the three roles as its target users.
- [[prds/sundal]] — names the three roles as its target audience.
