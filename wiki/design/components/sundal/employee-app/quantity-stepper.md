---
title: Quantity stepper
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[surfaces/sundal/employee-app/record-a-purchase]]", "[[product:modules/sundal/employee-app]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The quantity stepper lets an employee change how many of an item they are adding, one step per tap. It stands where a typed number would otherwise go, so an employee never types a quantity. It appears on an item's card, where the Add button turns into the stepper, and beside each line in the cart.

Use it for the quantity of an item an employee adds to a purchase.
- Do keep it to one step per tap, with no press-and-hold repeat.
- Do stop + at the available stock.
- Do not show the stock number, ever.
- Do not use it for an item with none left. That card shows the "Out of stock" label and no stepper.
- Do not use it for the vendor's stock count. That is a number field with + and − buttons, which the vendor can type into.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The group that holds the other parts and is named for the item. |
| Add button | Optional | Shown in place of the other parts while the quantity is zero. Item cards have it, and cart lines never do. |
| Decrease button | Required once the quantity is 1 or more | A − button that lowers the quantity by one. |
| Quantity | Required once the quantity is 1 or more | The current quantity, shown between the buttons. It cannot be edited. |
| Increase button | Required once the quantity is 1 or more | A + button that raises the quantity by one. |
| Limit message | Optional | A line of text under the stepper, shown when + has stopped at the available stock. |
| Progress indicator | Optional | Shown on the tapped button while its step is in flight. |

## Variants

The component varies by where it sits. There is one size, and it is not set yet (see Open questions).

| Context | Quantity zero | Quantity 1 or more | − at quantity 1 |
|---|---|---|---|
| Item card | The Add button | − quantity + | The item leaves the cart and the card shows the Add button again |
| Cart line | Not shown, because the line is gone | − quantity + | The line is removed |

Content configurations: a quantity of one, two or three digits fits without wrapping. The stepper shows no item name, so a long item name does not change it.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions. The parts' spacing is not annotated for the same reason, except that − and + sit apart so that a tap hits only one of them.

## States

| State | Treatment |
|---|---|
| Add | Only the Add button shows, because the quantity is zero. |
| Default | − quantity + shows, with both buttons enabled. |
| At limit | + is disabled and the limit message shows under the stepper. − stays enabled. |
| Loading | The tapped button shows a progress indicator at full strength and ignores another tap, and the other buttons wait until the server answers. It is never shown as disabled dimming, which would read as "you cannot do this". |
| Error | The server could not save the step. The stepper returns to the state it had before the tap, and the surface shows its error message. |
| Focus | The focused button shows a visible focus indication. Its form waits for the design system. |

## Props / API

None documented yet.

## Behavior & interaction

- Tapping Add adds one of the item once the server confirms, and the Add button becomes − 1 +.
- Tapping + raises the quantity by one, and tapping − lowers it by one. Each tap is one step. Holding a button down does nothing more than one tap.
- The quantity is never typed. The employee app's own rule says an employee changes a quantity with + and − only ([[product:modules/sundal/employee-app]]).
- + stops at the available stock and adds nothing past it. The stock number never shows, only the limit message.
- While a step is in flight, the tapped button shows the Loading state and a second tap does nothing.
- If the phone is offline when a button is tapped, the surface shows its offline state and nothing changes on the server.
- At 320 px wide and up, the stepper keeps its parts on one line.
- No motion is specified.

## Accessibility

- The container is a group named for the item. Each button is named for what it does to which item, such as "Add Lays Classic", "Increase Lays Classic" and "Decrease Lays Classic".
- Focus runs through the buttons in reading order: − then + . Focus stays on the button the employee tapped, unless that button goes away: when − from 1 removes the item on a card, focus moves to that card's Add button, and on a cart line, to the next line's stepper, or to the total when no line follows.
- After the server confirms a step, a screen reader announces the new quantity, such as "Lays Classic, 2 in the cart". The limit message is announced when it appears.
- Text meets a contrast ratio of 4.5 to 1, and the buttons meet 3 to 1 against their background, except where disabled.
- A disabled + is never conveyed by color alone: the limit message states why.
- Every button is at least 24 by 24 CSS pixels, with − and + spaced apart so that one tap hits one button. The size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The visible strings are the Add button's label and the limit message. Everything else is a number.
- The Add button reads "Add", in sentence case.
- The limit message states that no more is available and never gives a number. Its wording is "No more of this item is available.", and the word for the thing waits on the vocabulary decision in Open questions.
- English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The Add button and the stepper are one component in two display states, because the flow turns the Add button into the stepper on the same card | proposed | |
| A step shows once the server confirms, and the tapped button shows a progress indicator and ignores a repeat tap | proposed | |
| − from 1 removes the item, on a card as on a cart line | proposed | |
| At the available stock + is disabled and the limit message shows, with no number | proposed | |
| The Add button reads "Add" in sentence case | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the stepper's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| What size are the stepper's buttons, and how far apart are − and +? | Shivani Erlewad | The design system page exists |
| What does the progress indicator look like, and where does it sit on the tapped button? | Shivani Erlewad | The design system page exists |
| Does a change show at once and then confirm, or wait for the server? The decision above proposes waiting. | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| Does the limit message say "item" or "snack"? The app's own messages use both. | Shivani Erlewad | The app's vocabulary for the thing an employee takes is settled |
| What does the focus indication look like? | Shivani Erlewad | The design system page exists |

## Related

- [[surfaces/sundal/employee-app/record-a-purchase]] — the surfaces that use the stepper, Category items and Cart.
- [[product:modules/sundal/employee-app]] — the module whose rule keeps quantity changes to + and −.
