---
title: Action bar
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The action bar holds a screen's one main action as a full-width button, fixed to the bottom of the screen directly above the tab bar, so the action is always in reach. The Cart screen uses it for Record purchase. It takes the place the cart bar has on the other screens, because the Cart screen is the cart.

Use it for the one action that finishes a screen's task.
- Do keep it to one button.
- Do not show it together with the cart bar. They take the same place.
- Do not use it for a secondary action. Those stay in the content.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | A strip fixed to the bottom of the screen, directly above the tab bar, inset from the screen's sides. |
| Action button | Required | One [[components/sundal/employee-app/button]], full width, with the screen's main action as its label. |

## Variants

None. The bar has one configuration. Its button's label and state vary with the screen.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Position | Fixed to the bottom, above the tab bar | `fixed-bottom`, the project token `size-bar-offset` |
| Inset | Spacing 3 from the screen's sides | `px-3` |
| Button width | The bar's full width | `d-grid` |

## States

| State | Treatment |
|---|---|
| Default | The button, ready to tap. |
| Busy | The button shows "Recording…" and ignores a second tap while the server saves. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `children` | Button | None | Required | The screen's main action: one button, which fills the bar's width. |

The button is a prop because a prototype links only a button. The definition is `design/components/action-bar.json`, with its markup in `design/components/action-bar.html`.

## Behavior & interaction

- The bar is fixed to the screen directly above the tab bar and does not scroll with the content. The content scrolls above it and ends clear of it.
- Tapping the button runs the action. Its rules belong to the surface that uses the bar.
- No motion is specified.

## Accessibility

- The bar is a region labeled "Actions".
- The button follows the button's own accessibility contract, in [[components/sundal/employee-app/button]].

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The button's label is a verb phrase in sentence case, such as "Record purchase". English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The screen's main action sits in a bar fixed to the bottom, above the tab bar, and not in the content, so it is always in reach | proposed | |
| The bar takes the cart bar's place on the Cart screen | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Should the total show in the bar beside the button? | Shivani Erlewad | A screen of the bar has been designed |

## Related

- [[components/sundal/employee-app/button]] — the control the bar holds.
- [[components/sundal/employee-app/cart-bar]] — the bar the action bar replaces on the Cart screen.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Cart screen uses the bar for Record purchase.
