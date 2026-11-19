---
title: Design system
type: design-system
template-version: 2
realizes:
  - "[[product:app-base]]"
sources: []
related: ["[[components/sundal/employee-app/action-bar]]", "[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/cart-line]]", "[[components/sundal/employee-app/category-card]]", "[[components/sundal/employee-app/detail-card]]", "[[components/sundal/employee-app/item-card]]", "[[components/sundal/employee-app/line-notice]]", "[[components/sundal/employee-app/message-block]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/purchase-line]]", "[[components/sundal/employee-app/quantity-stepper]]", "[[components/sundal/employee-app/screen]]", "[[components/sundal/employee-app/tab-bar]]", "[[components/sundal/employee-app/toast]]", "[[information-architecture/employee-app]]", "[[layout-patterns/employee-app-shell]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Overview

The Sundal design system is the set of tokens, components and rules that every employee-app screen draws on, so that the app looks and reads the same everywhere. The tokens live as design-token files in `design/tokens/`, which UX Studio reads and turns into the library the prototype uses. Each component has its own page under `components/`, and each screen's layout is a surface page. Blinkit, Zepto and Instamart are the references for the patterns, adapted to Sundal's rules: it has no payment, delivery, discounts or wishlist, and each entry holds one snack.

## Principles

None.

## Voice and tone

**Voice:** Plain, short and kind. The words are the ones a shop's regular would use: no jargon, no blame, no number the employee cannot act on, and never the stock count. Sentences start with a capital letter and have no "please". English only.

| Situation | Tone |
|---|---|
| Validation error | Not used: an employee types nothing, so no input can be wrong. Quantity is changed with + and − only. |
| System error | Calm and brief, with the way out: "Something went wrong. Try again." with Retry. It never says what broke. |
| Offline | Short and the same everywhere: "You're offline", with Retry. A toast says it when nothing is tapped, and a message block says it when the employee taps something that needs the server. |
| Warning | Says what changed and what happened to the quantity: "The price changed. Check the total." It never gives a number of items left. |
| Confirmation of a risky action | Not used: an employee cannot cancel, edit or void an entry, so no risky action is confirmed. |
| Success | One line that says what is now true: "Your purchase has been recorded". |
| Information | A short label or sentence, such as "3 items in this purchase". |
| Empty state | Says what is missing and what to do next: "Your cart is empty. Add snacks from the shop to record a purchase." |

## Foundations / tokens

The values of each group are in the token files in `design/tokens/`, edited in UX Studio's Foundations. This section is the index and the intent.

- **Color.** Primary is green, `#198754`, and it colors links, the Add button, the stepper, the cart bar and Record purchase. The other roles keep Bootstrap's defaults. Six pale tones, `category-yellow`, `-blue`, `-coral`, `-lavender`, `-peach` and `-teal`, color the category boxes so no two categories look alike and none repeats the primary. The page color and the card color are tokens of their own, `surface-page` and `surface-card`, both white.
- **Typography.** One system sans font. Every heading is bold. Every button label is semibold. A price is bold, an item name is semibold and descriptions are small, in the one muted text color. The smallest text is 14 px, badges included. Sizes follow Bootstrap's scale.
- **Spacing.** One side gutter and one gap between blocks, both 16 px, from the spacing scale. The screen frame owns the gutter, and the blocks of a screen sit in one stack.
- **Radius.** One corner radius, 16 px, for cards, boxes, photos, alerts and buttons, from the `border-radius` token. Pills and circles keep their shape.
- **Elevation.** Bootstrap's shadows: a soft shadow on the cart bar, the tab bar and the round Back button, and a light one on item cards.
- **Sizes.** A tap target is at least 44 px: buttons take it from the button padding token, and the round Back button from `size-round-button`. List photos are 64 px, cart bar photos 40 px overlapping by 12 px, and the chevron chip 36 px. The fixed bars sit 104 px above the bottom of the screen, and a screen leaves 168 px of room under its content.
- **Layout grid.** One compact width class, the phone, designed at 390 px. A grid of two columns with a 16 px gutter holds categories and items.
- **Iconography.** Inline icons that take the text color: a grid for Browse, a receipt for Logs, a person for Profile, an arrow for Back and a chevron on the cart bar. Each is decorative, with its meaning in the label beside it. No icon set is catalogued yet.
- **Motion.** None specified.
- **Imagery.** Photos of items and categories, as the vendor uploads them, shown in rounded squares or circles.

## Component index

- [[components/sundal/employee-app/action-bar]] — the bar that holds a screen's one main action at the bottom.
- [[components/sundal/employee-app/button]] — the control an employee taps to do something or to go somewhere.
- [[components/sundal/employee-app/cart-bar]] — the green pill above the tab bar that shows the cart and opens it.
- [[components/sundal/employee-app/cart-line]] — one item in the cart, with its stepper and price.
- [[components/sundal/employee-app/category-card]] — a category as a colored box with its name as a link.
- [[components/sundal/employee-app/detail-card]] — a white card of label and value rows.
- [[components/sundal/employee-app/item-card]] — one item in a category, with its photo and the control to add it.
- [[components/sundal/employee-app/line-notice]] — a short message under one line or card, about that item only.
- [[components/sundal/employee-app/message-block]] — the message that fills a screen with nothing else to show.
- [[components/sundal/employee-app/page-header]] — the title strip at the top of a screen, with a round Back button.
- [[components/sundal/employee-app/purchase-line]] — one item of a recorded purchase, with no control.
- [[components/sundal/employee-app/quantity-stepper]] — the Add button and the − quantity + control.
- [[components/sundal/employee-app/screen]] — the frame that sets the page color, the side gutter and the room for the fixed bars.
- [[components/sundal/employee-app/tab-bar]] — the floating bar that moves between Browse, Logs and Profile.
- [[components/sundal/employee-app/toast]] — the short message that says the phone is offline.

## Interaction patterns

- **Recording a purchase.** A category card opens its items, an item card's Add button becomes the stepper, the cart bar shows the cart and opens it, cart lines let the employee change quantities, and the action bar records the purchase. It composes the [[components/sundal/employee-app/category-card]], the [[components/sundal/employee-app/item-card]], the [[components/sundal/employee-app/quantity-stepper]], the [[components/sundal/employee-app/cart-bar]], the [[components/sundal/employee-app/cart-line]] and the [[components/sundal/employee-app/action-bar]], and it is tested with one item and many, and with a long name.
- **Offline.** A toast says "You're offline" when nothing is tapped, and a message block with Retry replaces the content when the employee taps something that needs the server. It composes the [[components/sundal/employee-app/toast]], the [[components/sundal/employee-app/message-block]] and the [[components/sundal/employee-app/button]].
- **Fixed bottom stack.** The cart bar, or the action bar on the Cart, sits directly above the tab bar, and the content ends clear of both. The page arrangement is the [[layout-patterns/employee-app-shell]].

## Governance & contribution

The designer owns and maintains the system, and approves its changes. A token changes in UX Studio's Foundations, after which the library and the prototypes are generated again. A component changes on its own page and in its definition together. A component is added only once a screen needs it, and one used by a second application moves out of the employee app's folder then. A component is removed by deprecating it first and naming its replacement. There is no changelog yet.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Primary is green, `#198754`, so links, Add, the stepper, the cart bar and Record purchase share one color | proposed | |
| Every rectangular corner takes one radius, 16 px, from the `border-radius` token | proposed | |
| One 16 px side gutter and one 16 px gap between blocks, from the spacing scale, owned by the screen frame | proposed | |
| A tap target is at least 44 px, from the button padding token and the size tokens | proposed | |
| The page and the cards are both white, each its own token, so either can change without touching the other | proposed | |
| Each category takes one of six pale tones, so no category repeats another or the primary | proposed | |
| One system font, bold headings, semibold buttons, bold prices and a 14 px minimum | proposed | |
| Components are built from Bootstrap's classes and the project's tokens only, so a token change restyles them | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Does the app need an icon catalog beyond the five icons in use, and which icon set does it draw from? | Shivani Erlewad | A screen needs an icon that is not among the five |
| How does a control whose button is stretched invisibly over a shape, such as the cart bar, the Back button and the category name, show keyboard focus? | Shivani Erlewad | A keyboard or screen reader test has been run |
| Should the stepper's limit message stay, or should an item at its limit show only the turned-off +? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| Does the app need a dark mode? | Shivani Erlewad | Employees are asked how they use the app |
| With the page and the cards both white, do the cards need a stronger edge? | Shivani Erlewad | A click test on a prototype has been run |

## Related

- [[components/sundal/employee-app/action-bar]] — the bar that holds a screen's one main action at the bottom.
- [[components/sundal/employee-app/button]] — the control an employee taps to do something or to go somewhere.
- [[components/sundal/employee-app/cart-bar]] — the green pill above the tab bar that shows the cart and opens it.
- [[components/sundal/employee-app/cart-line]] — one item in the cart, with its stepper and price.
- [[components/sundal/employee-app/category-card]] — a category as a colored box with its name as a link.
- [[components/sundal/employee-app/detail-card]] — a white card of label and value rows.
- [[components/sundal/employee-app/item-card]] — one item in a category, with its photo and the control to add it.
- [[components/sundal/employee-app/line-notice]] — a short message under one line or card, about that item only.
- [[components/sundal/employee-app/message-block]] — the message that fills a screen with nothing else to show.
- [[components/sundal/employee-app/page-header]] — the title strip at the top of a screen, with a round Back button.
- [[components/sundal/employee-app/purchase-line]] — one item of a recorded purchase, with no control.
- [[components/sundal/employee-app/quantity-stepper]] — the Add button and the − quantity + control.
- [[components/sundal/employee-app/screen]] — the frame that sets the page color, the side gutter and the room for the fixed bars.
- [[components/sundal/employee-app/tab-bar]] — the floating bar that moves between Browse, Logs and Profile.
- [[components/sundal/employee-app/toast]] — the short message that says the phone is offline.
- [[information-architecture/employee-app]] — the structure the screens sit in.
- [[layout-patterns/employee-app-shell]] — how a screen's regions are arranged.
