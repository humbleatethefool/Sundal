---
title: Purchase line
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/cart-line]]", "[[components/sundal/employee-app/detail-card]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The purchase line shows one item of a recorded purchase, with its price, quantity and line total. It has a rounded photo and the item's name, with the price and quantity beneath and the total on the right. It is the line the Purchase detail screen lists, and it holds no control, because a recorded purchase cannot change.

Use it for an entry in a recorded purchase.
- Do show the price of one item as it was when the purchase was recorded.
- Do not use it for an item in the cart. That is the cart line, which holds the stepper.
- Do not add a control to it. An employee cannot cancel or change an entry.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole line, with space above and below it. |
| Photo | Required | The item's picture, a rounded square at the start of the line. |
| Name | Required | The item's name, beside the photo, wrapping onto more lines when it must. |
| Detail | Required | The price of one item and the quantity under the name, in small gray text, such as "₹20 x 2". |
| Total | Required | The line's total in rupees, in bold at the end of the line. |

## Variants

None. The line has one configuration. Its content varies: a long name wraps, and a missing image shows a plain tile.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Photo | Square, rounded, at the list photo size, the same as the cart line | the project token `size-thumb`, `ratio-1x1`, `rounded` |
| Name | Semibold, tight line height, the same as a cart line's name | `fw-semibold`, `lh-sm` |
| Detail | Small, muted | `small`, `text-body-secondary` |
| Total | Bold | `fw-bold` |
| Spacing | Spacing 3 between the parts | `gap-3`, `py-2` |
| Minimum line width | 15 rem, so a line keeps its shape when its container sets no width | an inline `min-width` |

## States

| State | Treatment |
|---|---|
| Default | The photo, the name, the detail and the total. |
| Placeholder | A line-shaped placeholder shows while the purchase loads. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `name` | Text | None | Required | The item's name. |
| `detail` | Text | None | Required | The price of one item and the quantity, such as "₹20 x 2". |
| `total` | Text | None | Required | The line's total, such as "₹40". |
| `image` | Image address | None | Optional | The item's photo. Left out, the line shows a plain tile. |

The definition is `design/components/purchase-line.json`, with its markup in `design/components/purchase-line.html`.

## Behavior & interaction

- The line has no tap target and no control.
- The price is the price shown when the purchase was recorded, so a later price change never alters the line.
- No motion is specified.

## Accessibility

- The line is read as the item's name, its price, the quantity and the line's total.
- The photo carries empty alternative text, because the name already says what it shows.
- Text meets a contrast ratio of 4.5 to 1.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The name is the vendor's own text and shows in full, wrapping where it must. The detail reads the price, then "x", then the quantity. Prices show in rupees. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The line shows the price and quantity under the name and the line's total on the right, after the order lines of Blinkit, Zepto and Instamart | proposed | |
| The line shows no old price, unit or discount, because Sundal has none | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| How does a line show when the vendor has voided its entry? | Shivani Erlewad | The vendor's void screens are designed |

## Related

- [[components/sundal/employee-app/cart-line]] — the line an item has in the cart, before it is recorded.
- [[components/sundal/employee-app/detail-card]] — the card that follows the lines with the totals.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Purchase detail screen lists the lines.
