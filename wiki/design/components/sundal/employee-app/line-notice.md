---
title: Line notice
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/item-card]]", "[[surfaces/sundal/employee-app/cart]]", "[[surfaces/sundal/employee-app/category-items]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The line notice is a short message directly under one cart line or one item card, about that item only. It tells the employee that something changed or failed for that item. It leaves the rest of the screen as it is.

Use it for a message about a single item.
- Do place it directly under the item it is about.
- Do say what changed and what happened to the quantity.
- Do not show the stock number.
- Do not use it when the whole screen has nothing to show. That is the message block.
- Do not use it for the stepper's limit message, which the stepper owns.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The notice, attached under the line it is about. |
| Text | Required | One or two short sentences. |

## Variants

The notice varies by what it reports. The wording of each is supplied by the screen that uses it.

| Variant | Used when |
|---|---|
| Price changed | An item's price changed while the cart was open |
| Short stock | Not enough of an item is left, and its quantity was lowered |
| No longer available | An item was removed from the shop |
| Save failed | The server could not save a change to the item |

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Hidden | Nothing shows under the line. |
| Shown | The text shows directly under the line. |

## Props / API

None documented yet.

## Behavior & interaction

- The notice appears when the change or failure it reports happens, and the screen does not scroll or move focus to it.
- It sits under its own line and does not shift the other lines out of their order.
- It holds no action. The employee responds with the line's own controls, such as − to take an unavailable item out.
- No motion is specified.

## Accessibility

- The notice is announced when it appears, and focus stays where it was.
- The meaning is carried by the text, never by color alone.
- Text meets a contrast ratio of 4.5 to 1.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

Each notice says what changed and what happened to the quantity, in the reader's words, and never gives the stock number. It leaves out "please" and words that judge the reader. The wording follows the project's UX-writing standard. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The notice sits directly under the line it is about and does not move focus | proposed | |
| The notice has no action of its own | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the notice's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| How long does a notice stay, and does it go when the cart changes? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| Does the notice carry an icon? | Shivani Erlewad | The design system page exists |

## Related

- [[components/sundal/employee-app/item-card]] — the card the notice sits under on Category items.
- [[surfaces/sundal/employee-app/cart]] and [[surfaces/sundal/employee-app/category-items]] — the surfaces that show the notice.
