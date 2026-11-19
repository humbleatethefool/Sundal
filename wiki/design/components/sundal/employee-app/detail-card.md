---
title: Detail card
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/purchase-line]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The detail card is a white rounded card that lists facts as rows of a label and a value, with an optional title. The Purchase detail screen uses it for the purchase's totals and for the time it was recorded.

Use it for a short list of facts about one thing.
- Do keep each row to a label and one value.
- Do show a total as a strong row, in bold with a rule above it.
- Do not use it for something the employee can change. It holds no control.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | A white rounded card with space inside. |
| Title | Optional | A bold heading at the top of the card. |
| Row | Required | A label at the start and a value at the end, in muted text. |
| Strong row | Optional | A row in bold with a rule above it, for a total. |

## Variants

The card varies by whether it has a title and a strong row.

| Variant | Holds | Used for |
|---|---|---|
| Totals | Rows, with a strong row last | The item count and the total |
| Titled facts | A title and rows | "Purchase details" and the time it was recorded |

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Card | The card color, rounded, with padding and a faint border, so its edge shows on the white page | the project token `surface-card`, `rounded`, `p-3`, `border` |
| Title | Bold, small heading | `h6`, `fw-bold` |
| Row | Label and value at opposite ends, muted | `d-flex`, `justify-content-between`, `text-body-secondary` |
| Strong row | Bold, with a rule above | `fw-bold`, `border-top`, `mt-2`, `pt-2` |
| Label | Never wraps, so a long value cannot squeeze it | `flex-shrink-0` |
| Minimum card width | 15 rem, so a card keeps its shape when its container sets no width | an inline `min-width` |

## States

| State | Treatment |
|---|---|
| Default | The title, if any, then the rows. |
| Placeholder | A card-shaped placeholder shows while the purchase loads. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `title` | Text | None | Optional | The card's title. |
| `rows` | List of rows | None | Required | The rows. Each has a `label`, a `value` and, for a total, `strong` set. |

The definition is `design/components/detail-card.json`, with its markup in `design/components/detail-card.html`.

## Behavior & interaction

- The card has no tap target and no control.
- No motion is specified.

## Accessibility

- Each row is read as its label, then its value.
- A title is a heading, so a screen reader reaches the card by its title.
- Text meets a contrast ratio of 4.5 to 1.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

A label is a short noun in sentence case. A value is the fact itself: a number, a price in rupees or a date and time in Indian time. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The card lists label and value rows on white, with a bold total under a rule, after the bill and order cards of Blinkit, Zepto and Instamart | proposed | |
| The card holds no fee, discount or payment row, because Sundal has none | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Does a long value wrap, or does the label give way? | Shivani Erlewad | A screen of the card has been designed |

## Related

- [[components/sundal/employee-app/purchase-line]] — the lines the totals card follows.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Purchase detail screen shows the card.
