---
title: Toast
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

The toast is a short message that appears over a screen and leaves the screen as it is. The employee app uses it for one thing: when the phone goes offline, a toast says "You're offline" and nothing else on screen changes.

Use it to tell the employee something that needs no action and no change to the screen.
- Do keep it to a few words.
- Do not use it when the employee has tapped something that needs the server. The screen then shows the message block with Retry.
- Do not use it for a message about one item. That is the line notice.
- Do not use it for an error the employee must act on.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The small panel that appears over the screen. |
| Text | Required | A short message. |

## Variants

None. The employee app has one toast, the offline one. Its text is supplied by the module's offline rule.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Hidden | Nothing shows. |
| Shown | The text appears over the screen without moving it. |

## Props / API

None documented yet.

## Behavior & interaction

- The toast appears when the phone goes offline, on whatever screen the employee is on.
- It changes nothing else on screen, moves no focus and blocks no tap.
- How long it stays, and whether it shows again, is open under Open questions.
- No motion is specified.

## Accessibility

- The message is announced when it appears, without taking focus.
- The meaning is carried by the text, never by color alone.
- Text meets a contrast ratio of 4.5 to 1.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The text is the module's own wording, "You're offline". It leaves out "please" and "sorry". English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The toast appears over the screen and takes no focus | proposed | |
| The toast is used only for the offline message | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the toast's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| Where does the toast sit on the screen, given the cart bar and tab bar at the bottom? | Shivani Erlewad | A screen of the toast has been designed |
| How long does the toast stay, and does it go when the phone comes back online? | Shivani Erlewad | A screen of the toast has been designed |

## Related

- [[components/sundal/employee-app/message-block]] — the block shown instead when the employee taps something that needs the server while offline.
- [[surfaces/sundal/employee-app/cart]], [[surfaces/sundal/employee-app/categories]], [[surfaces/sundal/employee-app/category-items]] and [[surfaces/sundal/employee-app/purchase-detail]] — the surfaces on which the toast can appear.
