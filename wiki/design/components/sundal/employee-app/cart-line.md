---
title: Cart line
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/item-card]]", "[[components/sundal/employee-app/line-notice]]", "[[components/sundal/employee-app/quantity-stepper]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The cart line shows one item in the employee's purchase cart, with its quantity stepper and price. It has a rounded photo, the item's name, the stepper with the price under it, and room beneath for a notice about that line. It is the line the Cart screen lists, and it is where an employee changes a quantity before recording.

Use it for an item in the cart.
- Do keep the stepper and the price in the same place on every line.
- Do show a notice about this item directly under its line.
- Do not use it for an item in a category's list. That is the item card.
- Do not show the stock number.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole line, with space above and below it. |
| Photo | Required | The item's picture, a rounded square at the start of the line. |
| Name | Required | The item's name, in semibold text beside the photo, wrapping onto more lines when it must. |
| Stepper | Required | The [[components/sundal/employee-app/quantity-stepper]] at the end of the line. |
| Price | Required | The price of one item, in rupees, in small semibold text under the stepper. |
| Notice slot | Optional | A [[components/sundal/employee-app/line-notice]] directly under the line, when something about this item changed. |

## Variants

None. The line has one configuration. Its content varies: a long name wraps, a missing image shows a plain tile, and the notice slot is empty until a notice applies.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Photo | Square, rounded, at the list photo size | the project token `size-thumb`, `ratio-1x1`, `rounded` |
| Name | Semibold, tight line height | `fw-semibold`, `lh-sm` |
| Price | Bold, at the body size, the same as a purchase line's total | `fw-bold` |
| Gaps | Spacing 3 between the parts, spacing 1 above the notice | `gap-3`, `mt-1` |
| Minimum line width | 15 rem, so a line keeps its shape when its container sets no width | an inline `min-width` |

## States

| State | Treatment |
|---|---|
| Default | The photo, the name, the stepper and the price. |
| With a notice | A line notice appears directly under the line, about this item only. |
| At limit | The stepper turns + off, and the line shows the limit message under it. |
| Placeholder | A line-shaped placeholder shows while the cart loads. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `name` | Text | None | Required | The item's name. |
| `price` | Text | None | Required | The price of one item, such as "₹20". |
| `image` | Image address | None | Optional | The item's photo. Left out, the line shows a plain tile. |
| `children` | Control | None | Required | The line's quantity stepper. |
| `notice` | Notice | None | Optional | A line notice about this item. Left empty when there is none. |

The definition is `design/components/cart-line.json`, with its markup in `design/components/cart-line.html`.

## Behavior & interaction

- The line has no tap target of its own. The stepper is its only control.
- Lowering the quantity from 1 with − removes the line.
- The price stays the price of one item, as shown when the item was added. The Cart's total is on the Cart screen.
- A notice appears directly under the line it is about, and leaves when the employee has dealt with it.
- No motion is specified.

## Accessibility

- The line is a group named for the item.
- The photo carries empty alternative text, because the name already says what it shows.
- Text meets a contrast ratio of 4.5 to 1.
- The stepper follows its own accessibility contract, in [[components/sundal/employee-app/quantity-stepper]].

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The name is the vendor's own text and shows in full, wrapping where it must. The price shows in rupees. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The photo sits at the start of the line, the name beside it, and the stepper with the price under it at the end, after the cart lines of Blinkit, Zepto and Instamart | proposed | |
| The line shows no stock count, no old price, no unit and no wishlist action, which the reference lines show, because Sundal has no stock display, discounts or wishlist | proposed | |
| A notice about an item shows directly under that item's line | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Does the price under the stepper show the price of one item or the line's total? | Shivani Erlewad | A screen of the line has been designed |

## Related

- [[components/sundal/employee-app/item-card]] — the card an item has in a category's list.
- [[components/sundal/employee-app/line-notice]] — the message shown directly under a line.
- [[components/sundal/employee-app/quantity-stepper]] — the control at the end of the line.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Cart screen lists the lines.
