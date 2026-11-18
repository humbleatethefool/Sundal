---
title: Button
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:modules/sundal/employee-app]]"
sources: []
related: ["[[components/sundal/employee-app/message-block]]", "[[surfaces/sundal/employee-app/cart]]", "[[surfaces/sundal/employee-app/categories]]", "[[surfaces/sundal/employee-app/category-items]]", "[[surfaces/sundal/employee-app/purchase-detail]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The button is the control an employee taps to do something or to go somewhere on a screen. It carries a short label naming the action. The employee app uses it for Record purchase, Retry and Browse snacks.

Use it for an action that is not part of another component.
- Do give a surface at most one primary button, for its main commitment.
- Do label it with a verb for what it does, in sentence case.
- Do not use it for the Add, − and + controls, which belong to the quantity stepper.
- Do not use it for moving between the app's areas. The tab bar does that.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The tappable shape. |
| Label | Required | A short text naming the action. |
| Progress indicator | Optional | Shown while the button's action is in flight. |

## Variants

The button varies along these dimensions.

| Dimension | Values | Used for |
|---|---|---|
| Emphasis | Primary, secondary | Primary for the surface's main commitment, Record purchase. Secondary for Retry and Browse snacks. |
| Width | Full width, fits its label | Full width for Record purchase. Retry and Browse snacks fit their label. |

Content configuration: a label that is too long for one line wraps. Labels are kept short so it does not.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The label in its emphasis. |
| Pressed | Feedback while the employee's finger is on the button. Its form waits for the design system. |
| Focus | A visible focus indication. Its form waits for the design system. |
| Loading | The label changes to the action in progress, such as "Recording…", with a progress indicator at full strength. The button ignores another tap and is never shown as disabled dimming. |

A failure is shown by the screen, not the button. A button for an action that cannot be taken is hidden and never disabled, as Record purchase is on an empty cart.

## Props / API

None documented yet.

## Behavior & interaction

- Tapping the button starts its action once.
- While the action is in flight the button blocks a second tap, so Record purchase can never be sent twice.
- A failure leaves the screen with its error message, and the button returns to its default state.
- If the phone is offline when the button is tapped, the screen shows its offline state.
- No motion is specified.

## Accessibility

- The button is a button, named by its label. A loading label such as "Recording…" is announced as it appears.
- Text meets a contrast ratio of 4.5 to 1, and the container meets 3 to 1 against its background.
- The button is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.
- The emphasis is never shown by color alone.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

A label names the action with a verb, in sentence case, with no article and no "Submit" or "OK". The wording follows the project's UX-writing standard. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The button has primary and secondary emphasis, and full-width and label-width forms | proposed | |
| A button with an action in flight keeps full strength and shows a progress indicator | proposed | |
| A button for an action that cannot be taken is hidden, not shown disabled. The quantity stepper is the exception: it keeps + visible but disabled at the stock limit, so its limit message can say why | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the button's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| What size is the button, and how does the progress indicator look? | Shivani Erlewad | The design system page exists |
| Does Browse snacks read as a secondary button or as a link? | Shivani Erlewad | A screen of the empty cart has been designed |

## Related

- [[components/sundal/employee-app/message-block]] — the block whose action is a button.
- [[surfaces/sundal/employee-app/cart]], [[surfaces/sundal/employee-app/categories]], [[surfaces/sundal/employee-app/category-items]] and [[surfaces/sundal/employee-app/purchase-detail]] — the surfaces that use Record purchase, Retry and Browse snacks.
