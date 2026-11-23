---
title: Employee — Record a purchase
type: user-journey
template-version: 2
actor: "[[product:personas/employee]]"
scenario: Record a purchase
roles: ["employee"]
sources: []
related: ["[[information-architecture/employee-app]]", "[[product:flows/sundal/employee-app/purchase-log]]", "[[product:flows/sundal/employee-app/record-a-purchase]]", "[[product:flows/sundal/employee-app/sign-in]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]", "[[product:prds/sundal]]"]
created: 2026-11-17
updated: 2026-11-23
owner: design
authorship: curated
origination: originate
confidence: low
---

## Actor & scope

This journey follows an employee from taking snacks at the shop to recording the purchase and checking it later. The employee ([[product:personas/employee]]) works at a company the vendor serves and wants to record their own purchase quickly on their own phone, so that no colleague has to record it for them. The journey starts when the employee takes a snack at the shop and ends when they can see the recorded purchase in their own list. The employee may record at the shop or at any other time and place, wherever the phone has a connection. No research backs it yet, so every stage rests on assumptions, each listed under Open questions.

## Stages

### Take snacks at the shop
- **Id** — take-snacks
- **Actions** — The employee takes one or more snacks from the vendor's shop. The vendor is often busy with tea or other work, so nobody records what the employee took unless the employee does. The employee may record straight away or later.
- **Flows** — Outside the product.
- **Touchpoints** — The vendor's shop. The vendor, who is usually busy.
- **Mindset** — The employee wants to take the snack and get on with their day. This describes the persona's goal of recording quickly and easily and rests on no research.
- **Pain points** — Today another employee in the company records everyone's purchases for the day, so what an employee took depends on someone else writing it down.
- **Opportunities** — None.
- **Evidence** — Assumption: the employee takes snacks first and records them afterwards; Assumption: the employee wants to leave the shop quickly after taking a snack
- **Next** — sign-in, choose-snacks

### Sign in
- **Id** — sign-in
- **Actions** — An employee who is signed out opens the app, enters their mobile number and then the OTP they receive. An employee the app already keeps signed in skips this stage. An employee on a new phone signs in the same way, with their mobile number and an OTP.
- **Flows** — [[product:flows/sundal/employee-app/sign-in]]
- **Touchpoints** — The employee's own phone.
- **Mindset** — The employee wants to get past sign-in and start recording. This rests on no research.
- **Pain points** — None. An employee signs in with their mobile number and an OTP on any phone, so moving to a new phone is the same sign-in.
- **Opportunities** — None.
- **Evidence** — Assumption: most visits skip sign-in because the app keeps the employee signed in
- **Next** — None.

### Choose snacks
- **Id** — choose-snacks
- **Actions** — The employee opens the vendor's categories, opens the one that holds what they took and adds each item to the purchase cart with ADD, then adjusts the quantity with + and −. An item with none left shows "Out of stock" and cannot be added.
- **Flows** — [[product:flows/sundal/employee-app/record-a-purchase]]
- **Touchpoints** — The employee's own phone. The employee's memory of what they took, when they record away from the shop.
- **Mindset** — The employee wants to find what they took without typing or hunting through the list. This rests on the app's rule that quantity changes by + and − only and on no research.
- **Pain points** — An item the employee took can show "Out of stock" and cannot be added, because walk-in cash sales are not recorded or because another employee recorded the last one first. An employee who records later must remember what and how many they took.
- **Opportunities** — None.
- **Evidence** — Assumption: the employee knows which category holds the snack they took; Assumption: an item showing "Out of stock" after the employee took it happens often enough to matter; Assumption: an employee who records later can remember what they took
- **Next** — None.

### Review and record
- **Id** — review-and-record
- **Actions** — The employee opens the cart from the cart bar, checks each item, its quantity and the total, changes a quantity if needed and taps Record purchase. If a price, an item or the stock changed while the cart was open, a notice appears under the item and the employee taps Record purchase again. Once the server confirms, the employee sees their purchase.
- **Flows** — [[product:flows/sundal/employee-app/record-a-purchase]]
- **Touchpoints** — The employee's own phone, with a connection, since every screen needs the internet.
- **Mindset** — The employee wants to know the purchase is recorded and correct. This rests on no research.
- **Pain points** — A changed price or short stock means one more tap before anything is recorded. A failed save records nothing and shows "Something went wrong. Try again." An employee without a connection sees "You're offline" with Retry and records nothing until the phone is back online.
- **Opportunities** — None.
- **Evidence** — Assumption: the employee reads the cart total before recording; Assumption: a changed price or short stock while the cart is open is rare; Assumption: employees often have a connection wherever they record
- **Next** — None.

### Look back at purchases
- **Id** — look-back
- **Actions** — Later, the employee opens Logs to see the purchases they recorded and opens one to see its lines, quantities, prices and total.
- **Flows** — [[product:flows/sundal/employee-app/purchase-log]]
- **Touchpoints** — The employee's own phone.
- **Mindset** — The employee wants to check what they recorded, all the more because they cannot cancel an entry. This rests on no research.
- **Pain points** — An employee cannot cancel an entry. A wrong line stays until the vendor voids it, and the app gives the employee no way to ask for that.
- **Opportunities** — None.
- **Evidence** — Assumption: employees check their past purchases; Assumption: employees record wrong lines often enough that not being able to cancel one matters
- **Next** — None.

## Cross-stage insights

- The time and place of recording are open. The employee may record at the shop, wanting it quick, or later and elsewhere, relying on memory and on a connection (take-snacks, choose-snacks, review-and-record). The stages must hold for both.
- A purchase is final once recorded. review-and-record can stop a wrong price or short stock before it is saved, and look-back shows a wrong line the employee cannot undo (review-and-record, look-back).
- Every stage the product carries out links its task flow: sign-in, choose-snacks, review-and-record and look-back.

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| take-snacks: Does the employee record straight away or later, and where are they when they do? | Shivani Erlewad | A shop visit with employees is done |
| sign-in: How often is an employee signed out? | Shivani Erlewad | The sign-in screens are designed and employees have been asked |
| choose-snacks: Does the employee know which category holds their snack, can they remember what they took when they record later, and how often does a snack they took show "Out of stock"? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| review-and-record: Does the employee read the cart before recording, how often does a notice appear, and do they have a connection where they record? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| look-back: Do employees check past purchases, and how often is a recorded line wrong? | Shivani Erlewad | The vendor has voided entries for some time or employees have been asked |
