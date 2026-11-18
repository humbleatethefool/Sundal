---
title: Category card
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The category card shows one of the vendor's categories as a tappable card, with the category's image above its name. It is the card the Categories screen lays out in a grid. Tapping it opens that category's items.

Use it for a category in the grid of categories.
- Do keep it to the image and the name.
- Do not use it for an item. An item has a description, a price and an action, and has its own card.
- Do not add a separate button. The whole card is the tap target.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole card, which is one tap target. |
| Image | Required | The category's picture, above the name. |
| Name | Required | The category's name, beneath the image. |

## Variants

None. The card has one configuration. Its content varies: a category whose image is missing or fails to load shows a plain tile in the image's place, and a long name wraps.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The image above the name. |
| Pressed | Feedback while the employee's finger is on the card. Its form waits for the design system. |
| Focus | A visible focus indication. Its form waits for the design system. |
| Placeholder | A card-shaped placeholder shows while the categories load. |

## Props / API

None documented yet.

## Behavior & interaction

- Tapping anywhere on the card opens that category's items.
- The card takes its width from the grid it sits in, and cards in one grid share one size and one image shape.
- A long name wraps onto more lines.
- No motion is specified.

## Accessibility

- The card is one control, named for the category. The image carries empty alternative text, because the name already says what it shows.
- Text meets a contrast ratio of 4.5 to 1, and the card's edge meets 3 to 1 against the screen behind it.
- The card is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The name is the vendor's own text and shows in full, wrapping where it must. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The card shows the image above the name, with no item count | proposed | |
| The whole card is the tap target, with no separate button | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the card's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| What shape and size is the category image, and how many lines may a name wrap onto? | Shivani Erlewad | The design system page exists |
| Is a category image required when the vendor creates a category? | Shivani Erlewad | The vendor's catalog screens are designed |

## Related

- [[surfaces/sundal/employee-app/record-a-purchase]] — the Categories surface that lays the cards out.
