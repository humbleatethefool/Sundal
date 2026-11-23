---
title: Item card
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/line-notice]]", "[[components/sundal/employee-app/quantity-stepper]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The item card shows one item in a category as a tall card, with a control for adding it. It has the photo on top, then the price, name and description, with the control overlapping the photo's bottom-right edge. It is the card the Category items screen lays out in a grid. It is where an employee decides what they took.

Use it for an item in a category's list.
- Do keep the control in the same place on every card.
- Do show "Out of stock" in place of the control when the item has none left.
- Do not show the stock number.
- Do not use it for a category. A category has its own card.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole card: white, with rounded corners and a soft shadow. |
| Image | Required | The item's photo, across the top of the card. |
| Price | Required | The price of one item, in rupees, in bold large text under the photo. |
| Name | Required | The item's name, in semibold text under the price. |
| Description | Required | The item's short description, in small gray text under the name. |
| Action slot | Required | Overlaps the photo's bottom-right edge, on a white backing. Holds the Add button, the [[components/sundal/employee-app/quantity-stepper]] or the "Out of stock" label, one at a time. |

## Variants

The card varies by what its action slot holds.

| Variant | Action slot holds | When |
|---|---|---|
| In stock | The Add button | The item has stock and is not in the cart |
| In the cart | The quantity stepper | The item is in the cart |
| Out of stock | The "Out of stock" label | The item has none left |

Content configurations: an item whose image is missing or fails to load shows a plain tile in the image's place. A long name wraps, and a long description wraps in full.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Card | White, rounded, soft shadow, no border | `card`, `rounded`, `shadow-sm`, `border-0` |
| Image | 4 to 3, filling the top, cropped to fit | `ratio-4x3`, `object-fit-cover` |
| Price | Bold, large | `fw-bold`, `fs-5` |
| Name | Semibold, tight line height | `fw-semibold`, `lh-sm` |
| Description | Small, muted | `small`, `text-body-secondary` |
| Action slot | Centered on the photo's bottom edge, 8 px from the right, backed in the card color | `top-100`, `translate-middle-y`, `me-2`, the project token `surface-card` |
| Card fill | The card color | the project token `surface-card` |
| Minimum card width | 9 rem, so a card keeps its shape when its container sets no width | an inline `min-width` |
| Text width | Follows the card, never the text, so long text wraps and does not widen the card | an inline `width` of 0 with a `min-width` of 100% |

The image's crop, the card's padding and the action slot's inset have no fitting token, so they are recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The image, name, description and price, with the action slot as its variant sets it. |
| At limit | The stepper shows its limit state and its limit message appears under the card. |
| Out of stock | The label replaces the control. The image and text stay at full contrast. |
| Placeholder | A card-shaped placeholder shows while the items load. |
| Error | A message under the card, in the [[components/sundal/employee-app/line-notice]], when the server could not save a change. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `name` | Text | None | Required | The item's name. |
| `description` | Text | None | Required | The item's short description. |
| `price` | Text | None | Required | The price of one item, such as ₹20. |
| `image` | Image address | None | Optional | The item's photo. Left out, the card shows a plain tile. |
| `children` | Control | None | Required | The action slot: the Add button, the quantity stepper or the Out of stock badge, one at a time. |

The definition is `design/components/item-card.json`, with its markup in `design/components/item-card.html`.

## Behavior & interaction

- The card has no tap target of its own. The Add button or the stepper in the action slot is its only control.
- Tapping Add turns the Add button into the stepper once the server confirms.
- If the server reports that the item has none left, the card shows "Out of stock".
- A change to the quantity shows the stepper's Loading state on the tapped button.
- Cards in one list share one size and one image shape.
- No motion is specified.

## Accessibility

- The card is a group named for the item, and "Out of stock" is read as part of it.
- The image carries empty alternative text, because the name already says what it shows.
- Text meets a contrast ratio of 4.5 to 1, including on an out-of-stock card, and the card's non-text parts meet 3 to 1 against their background.
- The controls in the action slot follow the stepper's own accessibility contract.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The name and description are the vendor's own text and show in full, wrapping where they must. The price shows in rupees. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The photo sits on top, with the price, name and description stacked under it, in a two-column grid of tall cards, after the product cards of Blinkit, Zepto and Instamart | proposed | |
| The action slot overlaps the photo's bottom-right edge on a white backing, so the control is in the same place on every card | proposed | |
| The card shows no stock count, no old price and no delivery time, which the reference cards show, because employees never see the stock number and Sundal has no discount or delivery | proposed | |
| The action slot sits in the same place on every card | proposed | |
| An out-of-stock card keeps full contrast and shows "Out of stock" in place of the control | proposed | |
| The card itself opens nothing, because the app has no item detail screen | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| What shape and size is the item image? | Shivani Erlewad | The design system page exists |
| How many lines may a name and a description wrap onto before the card grows too tall for its row? | Shivani Erlewad | A screen of the card has been designed |
| Should the card open an item detail? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |

## Related

- [[components/sundal/employee-app/line-notice]] — the message shown under the card when a change could not be saved.
- [[components/sundal/employee-app/quantity-stepper]] — the control the action slot holds once the item is in the cart.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Category items screen lists the cards.
