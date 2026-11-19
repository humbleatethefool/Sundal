---
title: Cart bar
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/quantity-stepper]]", "[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The cart bar is a green pill that shows an employee what their purchase cart holds, with photos of the first items, the item count and the total, and opens the Cart. The shell places it. It is hidden while the cart is empty, and appears the moment the first item is added.

Use it to keep the cart in sight while the employee browses.
- Do show it while the cart holds at least one item, on Browse, Logs and Profile.
- Do keep its count and total current as the cart changes.
- Do not show it while the cart is empty.
- Do not show it on the Cart screen, which is the cart, or on the sign-in screens.
- Do not use it to record the purchase. Record purchase is on the Cart screen.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole bar, which is one tap target: a fully rounded pill with a soft shadow, centered above the tab bar and only as wide as its content. |
| Item photos | Required | The photos of the first three items in the cart, round, overlapping and ringed in white. A cart of one item shows one photo, and a cart of two shows two. |
| Label | Required | The words "View cart", in bold white. |
| Item count and total | Required | How many items the cart holds and their price in rupees, in smaller text under the label, such as "3 items · ₹95". |
| Chevron | Required | A chevron in a darker round button at the end of the pill, which shows that a tap opens the Cart. |

## Variants

None. The bar has one configuration. Its count and total vary with the cart.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Container fill | The primary color, green in the design system | `bg-primary` |
| Container corners | Fully rounded | `rounded-pill` |
| Container shadow | Soft shadow | `shadow` |
| Text | White | `text-white` |
| Label | Bold, large | `fw-bold`, `fs-5` |
| Count and total | Small | `small` |
| Item photo | Small circle with a 2 px ring in the card color, overlapping the one before | `rounded-circle`, `border-2`, the project tokens `size-thumb-sm`, `size-thumb-overlap` and `surface-card` |
| Chevron button | A circle in a darker shade of the primary color | `rounded-circle`, the project token `size-chevron`, a mix of the primary color and black |
| Position | Fixed above the tab bar, centered | `fixed-bottom`, the project token `size-bar-offset` |

## States

| State | Treatment |
|---|---|
| Hidden | Nothing shows, because the cart is empty. |
| Shown | The item photos, the label "View cart", the item count and the total, and the chevron. |
| Pressed | Feedback while the employee's finger is on the bar. Its form waits for the design system. |
| Focus | A visible focus indication. Its form waits for the design system. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `summary` | Text | None | Required | The item count and total, such as "3 items · ₹95". |
| `image1` | Image address | None | Optional | The photo of the first item in the cart. |
| `image2` | Image address | None | Optional | The photo of the second item. Left out when the cart holds fewer than two items. |
| `image3` | Image address | None | Optional | The photo of the third item. Left out when the cart holds fewer than three items. |
| `children` | Button | None | Required | The button that opens the Cart: a button of the link variant labeled "View cart", stretched invisibly over the whole pill. |

The button is a prop because a prototype links only a button. The bar has no prop for hiding: an empty cart shows no bar. The definition is `design/components/cart-bar.json`, with its markup in `design/components/cart-bar.html`.

## Behavior & interaction

- Tapping anywhere on the bar opens the Cart.
- The bar appears when the first item is added, updates its count and total when a quantity changes, and goes when the last item is removed.
- The bar is fixed to the screen directly above the tab bar and does not scroll with the content.
- The cart is kept on the employee's account, so the bar shows the same items at the next sign-in.
- If the phone is offline when the bar is tapped, the screen shows its offline state.
- No motion is specified.

## Accessibility

- The bar is a region labeled "Cart", as the shell sets out, and holds one control that opens the Cart.
- The control is a button named "View cart", stretched invisibly over the pill. The item count and the total are read from the pill's own text.
- The invisible button shows no focus ring of its own. A visible focus indication waits for the design system.
- The item photos are decorative and carry empty alternative text, because the count and the total already say what the cart holds.
- A screen reader announces the new count and total after a change is confirmed.
- Text meets a contrast ratio of 4.5 to 1, and the control meets 3 to 1 against the screen behind it.
- The bar is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The bar reads "View cart" over a second line such as "1 item · ₹20". The count takes "item" for one and "items" for more. It follows the app's vocabulary and the project's UX-writing standard. The price shows in rupees. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The whole bar is the tap target, through a button labeled "View cart" stretched invisibly over the pill, so a prototype can link it | proposed | |
| The bar's label reads "View cart", the same words each surface's action row uses | proposed | |
| The bar is fixed directly above the floating tab bar while the content scrolls | proposed | |
| The bar takes its color from the design system's primary token, so a change to the token recolors it | proposed | |
| The bar is a fully rounded green pill, centered and only as wide as its content, after the cart bars of Blinkit, Zepto and Instamart | proposed | |
| The bar shows the photos of the first three items in the cart, overlapping, and a chevron that shows a tap opens the Cart | proposed | |
| The second line shows the count and the total together, such as "3 items · ₹95", because the employee checks the total before opening the Cart | proposed | |

Where the bar sits, and the screens on which it shows or hides, are recorded on [[layout-patterns/employee-app-shell]] and [[surfaces/sundal/employee-app/record-a-purchase]].

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Does the item count mean the number of different items or the total quantity? | Shivani Erlewad | A screen of the bar has been designed |
| Which items' photos show when the cart holds more than three: the first three added, or the three most recent? | Shivani Erlewad | A screen of the bar has been designed |

## Related

- [[components/sundal/employee-app/quantity-stepper]] — the control whose confirmed changes update the bar.
- [[layout-patterns/employee-app-shell]] — the shell that places the bar above the tab bar.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Cart screen the bar opens, and whose screens the bar shows on or hides from.
