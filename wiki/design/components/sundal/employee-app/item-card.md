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
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The item card shows one item in a category, with its image, name, description and price, and the control for adding it to the cart. It is the card the Category items screen lists. It is where an employee decides what they took.

Use it for an item in a category's list.
- Do keep the control in the same place on every card.
- Do show "Out of stock" in place of the control when the item has none left.
- Do not show the stock number.
- Do not use it for a category. A category has its own card.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole card. |
| Image | Required | The item's picture, at the start of the card. |
| Name | Required | The item's name. |
| Description | Required | The item's short description. |
| Price | Required | The price of one item, in rupees. |
| Action slot | Required | Holds the Add button, the [[components/sundal/employee-app/quantity-stepper]] or the "Out of stock" label, one at a time. |

## Variants

The card varies by what its action slot holds.

| Variant | Action slot holds | When |
|---|---|---|
| In stock | The Add button | The item has stock and is not in the cart |
| In the cart | The quantity stepper | The item is in the cart |
| Out of stock | The "Out of stock" label | The item has none left |

Content configurations: an item whose image is missing or fails to load shows a plain tile in the image's place. A long name wraps, and a long description wraps in full.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The image, name, description and price, with the action slot as its variant sets it. |
| At limit | The stepper shows its limit state and its limit message appears under the card. |
| Out of stock | The label replaces the control. The image and text stay at full contrast. |
| Placeholder | A card-shaped placeholder shows while the items load. |
| Error | A message under the card, in the [[components/sundal/employee-app/line-notice]], when the server could not save a change. |

## Props / API

None documented yet.

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
| The image sits at the start of the card with the name, description and price stacked beside it, to leave room for the description | proposed | |
| The action slot sits in the same place on every card | proposed | |
| An out-of-stock card keeps full contrast and shows "Out of stock" in place of the control | proposed | |
| The card itself opens nothing, because the app has no item detail screen | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the card's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| What shape and size is the item image? | Shivani Erlewad | The design system page exists |
| Does a very long description push the action slot out of its place on the card? | Shivani Erlewad | A screen of the card has been designed |
| Should the card open an item detail? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |

## Related

- [[components/sundal/employee-app/line-notice]] — the message shown under the card when a change could not be saved.
- [[components/sundal/employee-app/quantity-stepper]] — the control the action slot holds once the item is in the cart.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the Category items surface that lists the cards.
