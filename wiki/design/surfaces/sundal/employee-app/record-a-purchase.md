---
title: Record a purchase
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/record-a-purchase]]"
flows:
  - "[[product:flows/sundal/employee-app/record-a-purchase]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/category-card]]", "[[components/sundal/employee-app/item-card]]", "[[components/sundal/employee-app/line-notice]]", "[[components/sundal/employee-app/message-block]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/quantity-stepper]]", "[[components/sundal/employee-app/tab-bar]]", "[[components/sundal/employee-app/toast]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[domain:entities/cart]]", "[[domain:entities/category]]", "[[domain:entities/entry]]", "[[domain:entities/item]]", "[[domain:entities/purchase]]", "[[product:features/sundal/employee-app/record-a-purchase]]", "[[product:flows/sundal/employee-app/record-a-purchase]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-17
updated: 2026-11-17
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee records a purchase through these screens: the categories, a category's items, the cart and the purchase. The page specifies every surface in the feature's surface inventory.

## Platform scope

Mobile only, in one layout for the compact width class. One shared spec holds every surface on this page, with no per-platform deltas.

## Surfaces

### Categories (list)

The employee scans the vendor's categories and opens the one that holds the snack they took.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] categories
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] choose-snacks
- **Flow steps** — [[product:flows/sundal/employee-app/record-a-purchase]] S1, E1, T2
- **Layout patterns** — [[design:layout-patterns/employee-app-shell]]
- **Layout intent** — A page, because Categories is the root of the Browse tab and the first screen after sign-in. The shell supplies the [[design:components/sundal/employee-app/page-header]], the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]; this screen adds only what fills the content region. The content is a grid of two columns, one [[design:components/sundal/employee-app/category-card]] per category. The eye meets the page title first and the first row of cards second. The grid fills the width of the screen and scrolls inside the content region, and the shell's header and bars stay as the shell defines them. The header, the cart bar and the tab bar are the shell's, so their actions are not repeated here.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Categories | static | text, as the page title | Always |
  | Category image | [[domain:entities/category]] `image` | image, on the top of the card | One card per category |
  | Category name | [[domain:entities/category]] `name` | text, beneath the image | One card per category |

- **Input rules** — None. The employee fills in nothing on this screen; they only tap a card.
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | [[design:components/sundal/employee-app/category-card]], labeled with the category's name | nav | The categories have loaded | Opens that category's items | [[design:surfaces/sundal/employee-app/record-a-purchase#category-items-list]] |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The categories failed to load, or the phone is offline | Asks the server for the categories again and shows the loading state | — |

- **Resilience states** —
  - **Loading** — The whole content region loads. The category card's placeholder state shows while the categories arrive. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the vendor has added no categories. The [[design:components/sundal/employee-app/message-block]] fills the content region. Its title reads "No snacks listed yet" and its body reads "The vendor has not added any snacks. Check again later." The employee has no action to take, so none is offered. The cart bar appears when the cart already holds items from an earlier visit. A cleared list and no results cannot occur, because the employee cannot clear categories or search them.
  - **Error** — Two errors occur. When the server cannot return the categories, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens or on Retry, the message block shows "You're offline" with Retry, and nothing changes on the server. When the phone goes offline while the list is on screen, the [[design:components/sundal/employee-app/toast]] says "You're offline" and nothing else on screen changes. Both rules are the employee app's offline behavior in [[product:modules/sundal/employee-app]].
  - **Partial** — A single category shows as one card in the first column of the first row, with the rest of the grid empty. The card opens its items like any other. An image that is missing or fails to load follows the category card.
  - **Access-gated** — None. Only a signed-in employee reaches this screen, and every signed-in employee sees the same categories. A signed-out employee opens on the mobile number screen instead.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The categories arrive | The cards replace the placeholder cards |
  | Loading | Empty | The server returns no categories | The empty message replaces the placeholder cards |
  | Loading | Error | The server cannot return the categories, or the phone is offline | The error message and Retry replace the placeholder cards |
  | Error | Loading | The employee taps Retry | The error message gives way to the placeholder cards |
  | Ideal | Ideal | A category image fails to load | A plain tile replaces that image and the card stays tappable |
  | Ideal | Ideal | The phone goes offline | A toast says "You're offline", and the list stays as it is |

- **Accessibility** — The page title is the first heading and the cards follow it in reading order, left to right and then down, then the cart bar and the tab bar, which is also the focus order. The cards form one list, and each follows the category card's accessibility contract. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA. The screen announces "Loading categories" while the placeholder cards show, and the error and offline messages as they appear.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

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
- **Layout intent** — A page, because the employee moves into it from Categories and leaves it with Back, and it holds a list that scrolls. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the category's name as the page title and the Back control, the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]. The cart bar appears once the cart holds an item. The content is one column of [[design:components/sundal/employee-app/item-card]]s, because each card carries a description that needs width. The eye meets the page title first, then the first card's image and name. The list scrolls inside the content region. The header, the cart bar and the tab bar are the shell's, so their actions are not repeated here.
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

- **Resilience states** —
  - **Loading** — The whole content region loads. The item card's placeholder state shows while the items arrive. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the vendor has added no items to this category. The [[design:components/sundal/employee-app/message-block]] fills the content region. Its title reads "No snacks in this category yet" and its body reads "The vendor has not added any snacks here. Try another category." A category whose items are all out of stock is not empty, and shows its cards with "Out of stock". A cleared list and no results cannot occur, because the employee cannot clear items or search them.
  - **Error** — Four errors occur. When the server cannot return the items, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the employee taps Add, + or − while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the same step. When the server cannot save an add or a change, the card stays as it was and a [[design:components/sundal/employee-app/line-notice]] under it reads "Something went wrong. Try again." When the phone goes offline while the items are on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
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

- **Accessibility** — The page title is the first heading. The cards follow in reading order, then the cart bar and the tab bar, which is also the focus order. Each card follows the item card's accessibility contract, and the quantity stepper follows its own, in [[design:components/sundal/employee-app/quantity-stepper]]. The limit message and the error messages are announced as they appear. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA, including on out-of-stock cards.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

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
  | Record purchase, a primary [[design:components/sundal/employee-app/button]] | primary | The cart holds at least one item | Shows "Recording…" and blocks a second tap while the server saves. If a price, an item or the stock changed, or the save fails, the employee stays here with the error state below and nothing is recorded. | [[design:surfaces/sundal/employee-app/record-a-purchase#purchase-detail-detail]] |
  | + | secondary | The cart holds fewer of the item than are available | Raises the quantity by one per tap. The line and the total update once the server confirms. | — |
  | − | secondary | The line is in the cart | Lowers the quantity by one per tap. From 1, the line is removed. The total updates once the server confirms. | — |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The cart failed to load, the phone is offline, or a step failed | Repeats the step that failed | — |
  | Browse snacks, a [[design:components/sundal/employee-app/button]] | nav | The cart is empty | Opens the categories | [[design:surfaces/sundal/employee-app/record-a-purchase#categories-list]] |

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

### Purchase detail (detail)

The employee sees one recorded purchase: what they took, what it cost and when it was recorded.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] purchase-detail
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] review-and-record, look-back
- **Flow steps** — [[product:flows/sundal/employee-app/record-a-purchase]] S8
- **Layout patterns** — [[design:layout-patterns/employee-app-shell]]
- **Layout intent** — A page, because it is the whole outcome of recording and the whole of one purchase when the employee opens it later. It sits under the Logs tab, so Logs is the selected tab, whether the employee arrives from recording or from the Logs list. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the title "Purchase" and the Back control, the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]. The cart bar shows only when the cart holds items, as it does on every tab. The content runs top to bottom: a confirmation message when the employee has just recorded the purchase, then the time the purchase was recorded, then one line for each entry, then the total. A line shows the item's name, the quantity and the price. The eye meets the confirmation first when it shows, and otherwise the time. The total comes last and stands apart from the lines. The screen holds nothing to change: an employee cannot cancel an entry, so it offers no cancel, edit or void action. The list scrolls inside the content region.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Purchase | static | text, as the page title | Always |
  | Confirmation | system: the employee has just recorded this purchase | text reading "Your purchase has been recorded" | Only when the employee arrives from recording |
  | Time | [[domain:entities/purchase]] `time` | date and time, in Indian time, such as 17 Nov 2026, 3:42 pm | Always |
  | Item name | [[domain:entities/entry]] `item` | text | One line for each entry |
  | Quantity | [[domain:entities/entry]] `quantity` | whole number | One line for each entry |
  | Price | [[domain:entities/entry]] `price` | money, in rupees, for one item, as shown when the purchase was recorded | One line for each entry |
  | Total | [[domain:entities/purchase]] `total` | money, in rupees | Always |

- **Input rules** — None. The screen holds no input.
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The purchase failed to load, or the phone is offline | Asks the server for the purchase again and shows the loading state | — |

- **Resilience states** —
  - **Loading** — The whole content region loads. Placeholder lines in the shape of the entry lines show while the purchase arrives. The header and the tab bar are already in view.
  - **Empty** — None. A purchase holds at least one entry, because a cart needs at least one item to be recorded.
  - **Error** — Two errors occur. When the server cannot return the purchase, the message block fills the content region with Retry below it. When the employee has just recorded the purchase, it reads "Your purchase was recorded, but it could not be shown. Try again." and says nothing is lost, so the employee does not record it twice. When the employee opened the purchase from Logs, it reads "Something went wrong. Try again." When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the phone goes offline while the purchase is on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — A purchase with one entry shows one line, and the total equals that line's price times its quantity.
  - **Access-gated** — None. An employee reaches only their own purchases, so no other employee's purchase is ever shown.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The purchase arrives | The confirmation, the time, the lines and the total replace the placeholder lines |
  | Loading | Error | The server cannot return the purchase, or the phone is offline | The error message and Retry replace the placeholder lines |
  | Error | Loading | The employee taps Retry | The error message gives way to the placeholder lines |
  | Ideal | Ideal | The phone goes offline | A toast says "You're offline", and the screen stays as it is |

- **Accessibility** — The page title is the first heading. The confirmation is announced once as the screen opens. The time, the lines and the total follow in reading order, then the cart bar and the tab bar, which is also the focus order. Each line is read as the item's name, the quantity and the price. The total is read after the last line. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. Every surface on this page is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Each card shows the category's image above its name, with no item count | proposed | |
| The categories are a grid of two columns of cards | proposed | |
| The empty message reads "No snacks listed yet" with the body "The vendor has not added any snacks. Check again later." | proposed | |
| A failed load uses "Something went wrong" with the body "Try again." | proposed | |
| The items are one column of cards, with the image at the start of each card, to leave room for the description | proposed | |
| Prices show in rupees | proposed | |
| An out-of-stock card shows "Out of stock" in place of Add, at full contrast | proposed | |
| The Cart shows the lines, then the total, then Record purchase at the end of the content, not pinned over the bars | proposed | |
| The cart bar is hidden on the Cart screen, since the screen is the cart | proposed | |
| The cart bar shows on Purchase detail when the cart holds items, as it does on every tab | proposed | |
| The confirmation "Your purchase has been recorded" shows only when the employee arrives from recording, not when they open the purchase from Logs | proposed | |
| Purchase detail shows the time in Indian time, such as 17 Nov 2026, 3:42 pm | proposed | |
| When Purchase detail cannot load after recording, the message says the purchase was recorded, so the employee does not record it twice | proposed | |
| Purchase detail has no cancel, edit or void action | proposed | |
| The cart has no clear-all action: the employee takes each item out with − | proposed | |
| The notices under a line read "The price changed. Check the total.", "Not enough of this snack is available. The quantity was lowered." and "This snack is no longer available." | proposed | |
| An empty cart reads "Your cart is empty" with the body "Add snacks from the shop to record a purchase." and a Browse snacks action | proposed | |
| An empty category reads "No snacks in this category yet" with the body "The vendor has not added any snacks here. Try another category." | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| In what order are the categories listed: the order the vendor created them in, or alphabetical? | Shivani Erlewad | The vendor's catalog screens are designed |
| Is a category image required when the vendor creates a category, and what shape and size does it take? | Shivani Erlewad | The vendor's catalog screens are designed |
| How does a line show when the vendor has voided its entry? The Entry entity has no void state yet. | Shivani Erlewad | The vendor's void screens are designed |
| What does the employee do after recording: does Purchase detail offer a way to record another purchase, or do they leave by the tab bar? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| How does the employee leave the Cart? The shell puts Back on Items and Purchase only, so the Cart has the tab bar alone. | Shivani Erlewad | The shell's header is settled |
| The overview says an employee can empty the cart. Is a clear-all action needed beyond − on each item? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| In what order are the items listed within a category? | Shivani Erlewad | The vendor's catalog screens are designed |
| The flow describes changing a quantity with − only in the cart (A1). Does − on the items screen also remove an item at 1? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| The task flow's E5 message reads "Something went wrong. Please try again." The UX-writing standard leaves out "please". Should E5 change? | Shivani Erlewad | The flow's wording is next reviewed |
| The design system and its Voice and tone are not recorded. Do these messages follow a voice the system sets? | Shivani Erlewad | The design system page exists |
| Do the cart bar and the tab bar stay in view while the list scrolls? | Shivani Erlewad | The shell's open question on this is settled |

## Related

- [[components/sundal/employee-app/button]] — the control for Record purchase, Retry and Browse snacks.
- [[components/sundal/employee-app/cart-bar]] — the bar that shows the cart's count and total and opens the Cart.
- [[components/sundal/employee-app/category-card]] — the card each category shows as on Categories.
- [[components/sundal/employee-app/item-card]] — the card each item shows as on Category items.
- [[components/sundal/employee-app/line-notice]] — the message under a line or card about that item.
- [[components/sundal/employee-app/message-block]] — the block that fills a content region with an empty, error or offline message.
- [[components/sundal/employee-app/page-header]] — the header that shows each screen's title and Back.
- [[components/sundal/employee-app/quantity-stepper]] — the control that changes an item's quantity on Category items and Cart.
- [[components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[components/sundal/employee-app/toast]] — the message that says the phone is offline.
- [[information-architecture/employee-app]] — the sitemap node this surface sits on.
- [[journeys/employee-record-a-purchase]] — the journey whose choose-snacks stage this surface serves.
- [[layout-patterns/employee-app-shell]] — the frame this surface sits in.
- [[domain:entities/cart]] — the entity that holds the quantity an item has in the cart.
- [[domain:entities/category]] — the entity whose name and image each category card shows.
- [[domain:entities/entry]] — the entity whose item, quantity and price each line of a purchase shows.
- [[domain:entities/item]] — the entity whose image, name, description and price each item card shows.
- [[domain:entities/purchase]] — the entity whose time and total the purchase shows.
- [[product:features/sundal/employee-app/record-a-purchase]] — the feature this surface realizes.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the flow whose steps happen here.
- [[product:personas/employee]] — the person using the screen.
