---
title: Category items
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/record-a-purchase]]"
flows:
  - "[[product:flows/sundal/employee-app/record-a-purchase]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/item-card]]", "[[components/sundal/employee-app/line-notice]]", "[[components/sundal/employee-app/message-block]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/quantity-stepper]]", "[[components/sundal/employee-app/tab-bar]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[domain:entities/cart]]", "[[domain:entities/category]]", "[[domain:entities/item]]", "[[product:features/sundal/employee-app/record-a-purchase]]", "[[product:flows/sundal/employee-app/record-a-purchase]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

On the Category items screen the employee browses one category's items and adds the snacks they took to the cart.

## Platform scope

Mobile only, in one layout for the compact width class, with no per-platform deltas.

## Surfaces

### Category items (list)

The employee looks through the items in the category they opened and adds the snacks they took to the purchase cart.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] category-items
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] choose-snacks
- **Flow steps** — [[product:flows/sundal/employee-app/record-a-purchase]] S2, S3, S4, E3, T1
- **Layout patterns** — [[design:layout-patterns/employee-app-shell]]
- **Layout intent** — A page, because the employee moves into it from Categories and leaves it with Back, and it holds a list that scrolls. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the category's name as the page title and the Back control, the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]. The cart bar appears once the cart holds an item. The content is one column of [[design:components/sundal/employee-app/item-card]]s, because each card carries a description that needs width. The eye meets the page title first, then the first card's image and name. The list scrolls inside the content region. The header, the cart bar and the tab bar are the shell's, so their actions are not repeated here, except the cart bar's one action, which opens the Cart and is listed under Actions.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Category name | [[domain:entities/category]] `name` | text, as the page title | Always |
  | Item image | [[domain:entities/item]] `image` | image, at the start of the card | One card per item |
  | Item name | [[domain:entities/item]] `name` | text | One card per item |
  | Item description | [[domain:entities/item]] `description` | text, wraps in full | One card per item |
  | Price | [[domain:entities/item]] `price per item` | money, in rupees, for one item | One card per item |
  | Out of stock | derived from [[domain:entities/item]] `stock quantity` — shown in place of Add when the quantity is zero | badge reading "Out of stock" | The item has none left. The quantity itself never shows. |
  | Quantity in the cart | [[domain:entities/cart]] `lines` | number between the − and + buttons | The item is in the cart |
  | Limit message | system: the employee has reached the available stock | text under the card | The cart holds all that is available of the item |

- **Input rules** —

  | Field | Control | Required | Validation | Help | Default |
  |---|---|---|---|---|---|
  | Quantity | [[design:components/sundal/employee-app/quantity-stepper]] | Optional | + stops at the available stock, and the stepper's limit message shows under the card, checked when + is tapped | None, because the stock number is never shown | 1, when Add is tapped |

- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Add, in the [[design:components/sundal/employee-app/quantity-stepper]] | secondary | The item has stock and is not in the cart | Adds one of the item to the cart. Add becomes the − 1 + stepper once the server confirms, and while it waits the stepper shows its Loading state. The cart bar appears or updates its count and total. A failure leaves the card as it was and shows the error state. | — |
  | + | secondary | The cart holds fewer of the item than are available | Raises the quantity by one per tap. The cart bar updates once the server confirms. | — |
  | − | secondary | The item is in the cart | Lowers the quantity by one per tap. From 1, the item leaves the cart and the card shows Add again. The cart bar updates, and hides when the cart is empty. | — |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The items failed to load, the phone is offline, or an add or change failed | Repeats the step that failed | — |
  | View cart, in the shell's [[design:components/sundal/employee-app/cart-bar]] | nav | The cart holds at least one item | Opens the Cart. | [[design:surfaces/sundal/employee-app/cart#cart-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads. The item card's placeholder state shows while the items arrive. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the vendor has added no items to this category. The [[design:components/sundal/employee-app/message-block]] fills the content region. Its title reads "No snacks in this category yet" and its body reads "The vendor has not added any snacks here. Try another category." A category whose items are all out of stock is not empty, and shows its cards with "Out of stock". A cleared list and no results cannot occur, because the employee cannot clear items or search them.
  - **Error** — Four errors occur. When the server cannot return the items, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the employee taps Add, +, − or the cart bar while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the same step. When the server cannot save an add or a change, the card stays as it was and a [[design:components/sundal/employee-app/line-notice]] under it reads "Something went wrong. Try again." When the phone goes offline while the items are on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — A category with one item shows one card at the top of the content region. An image that is missing or fails to load follows the item card.
  - **Access-gated** — None. Only a signed-in employee reaches this screen, and every signed-in employee sees the same items.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The items arrive | The cards replace the placeholder cards |
  | Loading | Empty | The server returns no items | The empty message replaces the placeholder cards |
  | Loading | Error | The server cannot return the items, or the phone is offline | The error message and Retry replace the placeholder cards |
  | Error | Loading | The employee taps Retry on a load error | The error message gives way to the placeholder cards |
  | Ideal | Ideal | The employee taps Add and the server confirms | Add becomes − 1 +, and the cart bar appears or updates |
  | Ideal | Ideal | The cart holds all that is available of an item | The stepper shows its limit state, with its limit message under the card |
  | Ideal | Ideal | The server reports an item has none left when the employee adds it | The card shows "Out of stock" in place of Add or the stepper |
  | Ideal | Error | The employee taps Add, + or − while offline | The screen shows "You're offline" with Retry |
  | Error | Ideal | The employee taps Retry and the step succeeds | The screen returns with the step done |
  | Ideal | Cart | The employee taps the cart bar | The screen gives way to the Cart |

- **Accessibility** — The page title is the first heading. The cards follow in reading order, then the cart bar and the tab bar, which is also the focus order. Each card follows the item card's accessibility contract, and the quantity stepper follows its own, in [[design:components/sundal/employee-app/quantity-stepper]]. The limit message and the error messages are announced as they appear. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA, including on out-of-stock cards.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. The surface is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| A failed load uses "Something went wrong" with the body "Try again." | proposed | |
| The items are one column of cards, with the image at the start of each card, to leave room for the description | proposed | |
| Prices show in rupees | proposed | |
| An out-of-stock card shows "Out of stock" in place of Add, at full contrast | proposed | |
| An empty category reads "No snacks in this category yet" with the body "The vendor has not added any snacks here. Try another category." | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| In what order are the items listed within a category? | Shivani Erlewad | The vendor's catalog screens are designed |
| The flow describes changing a quantity with − only in the cart (A1). Does − on the items screen also remove an item at 1? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| The design system and its Voice and tone are not recorded. Do these messages follow a voice the system sets? | Shivani Erlewad | The design system page exists |
| Do the cart bar and the tab bar stay in view while the list scrolls? | Shivani Erlewad | The shell's open question on this is settled |

## Related

- [[components/sundal/employee-app/button]] — the control for Retry.
- [[components/sundal/employee-app/cart-bar]] — the bar that shows the cart's count and total and opens the Cart.
- [[components/sundal/employee-app/item-card]] — the card each item shows as.
- [[components/sundal/employee-app/line-notice]] — the message under a card about that item.
- [[components/sundal/employee-app/message-block]] — the block that fills the content region with an empty, error or offline message.
- [[components/sundal/employee-app/page-header]] — the header that shows the category's name and Back.
- [[components/sundal/employee-app/quantity-stepper]] — the control that changes an item's quantity.
- [[components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[information-architecture/employee-app]] — the sitemap node this surface sits on.
- [[journeys/employee-record-a-purchase]] — the journey whose choose-snacks stage this surface serves.
- [[layout-patterns/employee-app-shell]] — the frame this surface sits in.
- [[domain:entities/cart]] — the entity that holds the quantity an item has in the cart.
- [[domain:entities/category]] — the entity whose name and image each category card shows.
- [[domain:entities/item]] — the entity whose image, name, description and price each item card shows.
- [[product:features/sundal/employee-app/record-a-purchase]] — the feature this surface realizes.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the flow whose steps happen here.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screen.
