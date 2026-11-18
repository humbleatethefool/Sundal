---
title: Cart
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/record-a-purchase]]"
flows:
  - "[[product:flows/sundal/employee-app/record-a-purchase]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/line-notice]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/quantity-stepper]]", "[[components/sundal/employee-app/tab-bar]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/categories]]", "[[surfaces/sundal/employee-app/purchase-detail]]", "[[domain:entities/cart]]", "[[domain:entities/item]]", "[[product:features/sundal/employee-app/record-a-purchase]]", "[[product:flows/sundal/employee-app/record-a-purchase]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee checks the purchase cart and its total on the Cart screen, changes quantities if needed and records the purchase.

## Platform scope

Mobile only, in one layout for the compact width class, with no per-platform deltas.

## Surfaces

### Cart (list)

The employee checks what is in the purchase cart and its total, changes quantities if needed and records the purchase.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] cart
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] review-and-record
- **Flow steps** — [[product:flows/sundal/employee-app/record-a-purchase]] S5, S6, A1, E3, E4, E5
- **Layout patterns** — [[design:layout-patterns/employee-app-shell]]
- **Layout intent** — A page, because the employee opens it from the cart bar, and checking a list and its total takes the whole screen. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the title "Cart", and the [[design:components/sundal/employee-app/tab-bar]]. The [[design:components/sundal/employee-app/cart-bar]] is hidden here, since this screen is the cart. The content is one column with the cart's lines first, then the total, then Record purchase at the end of the content, so the employee reads down to the commitment. A line shows the item's name and price with the [[design:components/sundal/employee-app/quantity-stepper]] beside it, and nothing else, to keep the screen light. The eye meets the page title first, then the first line, and last the total and Record purchase, which is the only primary action. Record purchase is a full-width [[design:components/sundal/employee-app/button]] and sits below the total, not pinned over the bars. A [[design:components/sundal/employee-app/line-notice]] about a line appears directly under that line. The list scrolls inside the content region.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Cart | static | text, as the page title | Always |
  | Item name | [[domain:entities/item]] `name` | text | One line per item in the cart |
  | Price | [[domain:entities/item]] `price per item` | money, in rupees, for one item | One line per item in the cart |
  | Quantity | [[domain:entities/cart]] `lines` | number between the − and + buttons | One line per item in the cart |
  | Total | [[domain:entities/cart]] `total` | money, in rupees | The cart holds at least one item |
  | Notice | system: a price, an item or its stock changed while the cart was open | text under the line | The change applies to that line |

- **Input rules** —

  | Field | Control | Required | Validation | Help | Default |
  |---|---|---|---|---|---|
  | Quantity | [[design:components/sundal/employee-app/quantity-stepper]] | Optional | + stops at the available stock, and the stepper's limit message shows under the line, checked when + is tapped. − from 1 removes the line. | None, because the stock number is never shown | The quantity already in the cart |

- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Record purchase, a primary [[design:components/sundal/employee-app/button]] | primary | The cart holds at least one item | Shows "Recording…" and blocks a second tap while the server saves. If a price, an item or the stock changed, or the save fails, the employee stays here with the error state below and nothing is recorded. | [[design:surfaces/sundal/employee-app/purchase-detail#purchase-detail-detail]] |
  | + | secondary | The cart holds fewer of the item than are available | Raises the quantity by one per tap. The line and the total update once the server confirms. | — |
  | − | secondary | The line is in the cart | Lowers the quantity by one per tap. From 1, the line is removed. The total updates once the server confirms. | — |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The cart failed to load, the phone is offline, or a step failed | Repeats the step that failed | — |
  | Browse snacks, a [[design:components/sundal/employee-app/button]] | nav | The cart is empty | Opens the categories | [[design:surfaces/sundal/employee-app/categories#categories-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads, because the cart is kept on the employee's account. Placeholder lines in the shape of the cart lines show while it arrives. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the employee took the last item out with −. First use cannot occur, because the cart bar that opens this screen is hidden while the cart is empty. The message block fills the content region. Its title reads "Your cart is empty" and its body reads "Add snacks from the shop to record a purchase." Browse snacks sits below it.
  - **Error** — Five errors occur. When the cart cannot load, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the employee taps +, − or Record purchase while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the same step. When the server cannot save the purchase, the screen shows the E5 message from the flow, nothing is recorded, and the cart stays as it was, so the employee taps Record purchase again. When a price, an item or the stock changed while the cart was open (E4), a line notice appears under that line, the quantity is lowered, and nothing is recorded until the employee taps Record purchase again. The notice reads "The price changed. Check the total." for a changed price, "Not enough of this snack is available. The quantity was lowered." for short stock, and "This snack is no longer available." for a removed item, which the employee takes out with −. No notice shows the stock number. When the phone goes offline while the cart is on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — A cart with one line shows that line, with a total equal to its price times its quantity, and Record purchase below. The cart still shows the ideal layout.
  - **Access-gated** — None. Only a signed-in employee reaches this screen, and each employee sees only their own cart.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The cart arrives | The lines and the total replace the placeholder lines |
  | Loading | Error | The cart cannot load, or the phone is offline | The error message and Retry replace the placeholder lines |
  | Error | Loading | The employee taps Retry on a load error | The error message gives way to the placeholder lines |
  | Ideal | Ideal | The employee taps + or − and the server confirms | The quantity, the line and the total update |
  | Ideal | Empty | The employee takes the last item out with − | The empty message replaces the lines and the total, and Record purchase goes |
  | Ideal | Recording | The employee taps Record purchase | The button shows "Recording…" and cannot be tapped again |
  | Recording | Purchase detail | The server confirms | The screen gives way to the purchase detail |
  | Recording | Ideal | A price, an item or the stock changed | A notice appears under the line, the quantity is lowered, and the total updates |
  | Recording | Error | The phone is offline, or the server cannot save | The "You're offline" screen with Retry, or the E5 message, shows |

- **Accessibility** — The page title is the first heading. The lines follow in reading order, then the total, Record purchase and the tab bar, which is also the focus order. Each line is a group named for its item. The quantity stepper's accessibility contract applies, in [[design:components/sundal/employee-app/quantity-stepper]]. Record purchase follows the button's accessibility contract. The total is read before Record purchase. The line notice follows its own contract. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. The surface is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| A failed load uses "Something went wrong" with the body "Try again." | proposed | |
| Prices show in rupees | proposed | |
| The Cart shows the lines, then the total, then Record purchase at the end of the content, not pinned over the bars | proposed | |
| The cart bar is hidden on the Cart screen, since the screen is the cart | proposed | |
| The cart has no clear-all action: the employee takes each item out with − | proposed | |
| The notices under a line read "The price changed. Check the total.", "Not enough of this snack is available. The quantity was lowered." and "This snack is no longer available." | proposed | |
| An empty cart reads "Your cart is empty" with the body "Add snacks from the shop to record a purchase." and a Browse snacks action | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| How does the employee leave the Cart? The shell puts Back on Items and Purchase only, so the Cart has the tab bar alone. | Shivani Erlewad | The shell's header is settled |
| The overview says an employee can empty the cart. Is a clear-all action needed beyond − on each item? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| The task flow's E5 message reads "Something went wrong. Please try again." The UX-writing standard leaves out "please". Should E5 change? | Shivani Erlewad | The flow's wording is next reviewed |
| The design system and its Voice and tone are not recorded. Do these messages follow a voice the system sets? | Shivani Erlewad | The design system page exists |
| Do the cart bar and the tab bar stay in view while the list scrolls? | Shivani Erlewad | The shell's open question on this is settled |

## Related

- [[components/sundal/employee-app/button]] — the control for Record purchase, Retry and Browse snacks.
- [[components/sundal/employee-app/cart-bar]] — the bar the shell hides on this screen, since this screen is the cart.
- [[components/sundal/employee-app/line-notice]] — the message under a line about that item.
- [[components/sundal/employee-app/page-header]] — the header that shows the title Cart.
- [[components/sundal/employee-app/quantity-stepper]] — the control that changes an item's quantity.
- [[components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[information-architecture/employee-app]] — the sitemap node this surface sits on.
- [[journeys/employee-record-a-purchase]] — the journey whose review-and-record stage this surface serves.
- [[layout-patterns/employee-app-shell]] — the frame this surface sits in.
- [[surfaces/sundal/employee-app/categories]] — the surface Browse snacks opens.
- [[surfaces/sundal/employee-app/purchase-detail]] — the surface Record purchase opens.
- [[domain:entities/cart]] — the entity that holds the quantity an item has in the cart.
- [[domain:entities/item]] — the entity whose name and price each line shows.
- [[product:features/sundal/employee-app/record-a-purchase]] — the feature this surface realizes.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the flow whose steps happen here.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screen.
