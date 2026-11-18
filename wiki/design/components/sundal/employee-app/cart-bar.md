---
title: Cart bar
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/quantity-stepper]]", "[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/cart]]", "[[surfaces/sundal/employee-app/categories]]", "[[surfaces/sundal/employee-app/category-items]]", "[[surfaces/sundal/employee-app/purchase-detail]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The cart bar shows an employee what their purchase cart holds, with the item count and the total, and opens the Cart. The shell places it. It is hidden while the cart is empty, and appears the moment the first item is added.

Use it to keep the cart in sight while the employee browses.
- Do show it while the cart holds at least one item, on Browse, Logs and Profile.
- Do keep its count and total current as the cart changes.
- Do not show it while the cart is empty.
- Do not show it on the Cart screen, which is the cart, or on the sign-in screens.
- Do not use it to record the purchase. Record purchase is on the Cart screen.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole bar, which is one tap target. |
| Item count | Required | How many items the cart holds. |
| Total | Required | The price of everything in the cart, in rupees. |

## Variants

None. The bar has one configuration. Its count and total vary with the cart.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Hidden | Nothing shows, because the cart is empty. |
| Shown | The item count and the total. |
| Pressed | Feedback while the employee's finger is on the bar. Its form waits for the design system. |
| Focus | A visible focus indication. Its form waits for the design system. |

## Props / API

None documented yet.

## Behavior & interaction

- Tapping anywhere on the bar opens the Cart.
- The bar appears when the first item is added, updates its count and total when a quantity changes, and goes when the last item is removed.
- Whether the bar stays in view while the content scrolls is open under Open questions.
- The cart is kept on the employee's account, so the bar shows the same items at the next sign-in.
- If the phone is offline when the bar is tapped, the screen shows its offline state.
- No motion is specified.

## Accessibility

- The bar is a region labeled "Cart", as the shell sets out, and holds one control that opens the Cart.
- The control's name includes the item count and the total, such as "Cart, 2 items, 40 rupees".
- A screen reader announces the new count and total after a change is confirmed.
- Text meets a contrast ratio of 4.5 to 1, and the control meets 3 to 1 against the screen behind it.
- The bar is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The bar shows numbers, so its only wording is the word for the items counted. It follows the app's vocabulary and the project's UX-writing standard. The price shows in rupees. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The whole bar is the tap target | proposed | |

Where the bar sits, and the screens on which it shows or hides, are recorded on [[layout-patterns/employee-app-shell]], [[surfaces/sundal/employee-app/cart]], [[surfaces/sundal/employee-app/categories]], [[surfaces/sundal/employee-app/category-items]] and [[surfaces/sundal/employee-app/purchase-detail]].

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the bar's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| Does the item count mean the number of different items or the total quantity? | Shivani Erlewad | A screen of the bar has been designed |
| Do the cart bar and the tab bar stay in view while the content scrolls? | Shivani Erlewad | The shell's open question on this is settled |

## Related

- [[components/sundal/employee-app/quantity-stepper]] — the control whose confirmed changes update the bar.
- [[layout-patterns/employee-app-shell]] — the shell that places the bar above the tab bar.
- [[surfaces/sundal/employee-app/cart]], [[surfaces/sundal/employee-app/categories]], [[surfaces/sundal/employee-app/category-items]] and [[surfaces/sundal/employee-app/purchase-detail]] — the surfaces on which the bar shows or hides.
