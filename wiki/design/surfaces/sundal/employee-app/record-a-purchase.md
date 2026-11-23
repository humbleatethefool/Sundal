---
title: Record a purchase
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/record-a-purchase]]"
flows:
  - "[[product:flows/sundal/employee-app/purchase-log]]"
  - "[[product:flows/sundal/employee-app/record-a-purchase]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/action-bar]]","[[components/sundal/employee-app/button]]","[[components/sundal/employee-app/cart-bar]]","[[components/sundal/employee-app/cart-line]]","[[components/sundal/employee-app/category-card]]","[[components/sundal/employee-app/detail-card]]","[[components/sundal/employee-app/item-card]]","[[components/sundal/employee-app/line-notice]]","[[components/sundal/employee-app/message-block]]","[[components/sundal/employee-app/page-header]]","[[components/sundal/employee-app/purchase-line]]","[[components/sundal/employee-app/quantity-stepper]]","[[components/sundal/employee-app/screen]]","[[components/sundal/employee-app/tab-bar]]","[[components/sundal/employee-app/toast]]","[[information-architecture/employee-app]]","[[journeys/employee-record-a-purchase]]","[[layout-patterns/employee-app-shell]]","[[domain:entities/cart]]","[[domain:entities/category]]","[[domain:entities/item]]","[[domain:entities/purchase]]","[[product:entities/sundal/entry]]","[[product:features/sundal/employee-app/record-a-purchase]]","[[product:flows/sundal/employee-app/record-a-purchase]]","[[product:modules/sundal/employee-app]]","[[product:personas/employee]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-23
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee records a purchase across four screens. They scan the vendor's categories, add snacks from one category's items, check the cart and record it, then see the recorded purchase.

## Platform scope

Mobile only, in one layout for the compact width class, with no per-platform deltas.

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
- **Layout intent** — A page, because Categories is the root of the Browse tab and the first screen after sign-in. The shell supplies the [[design:components/sundal/employee-app/page-header]], the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]; this screen adds only what fills the content region. The content is a grid of two columns, one [[design:components/sundal/employee-app/category-card]] per category. The eye meets the page title first and the first row of cards second. The grid fills the width of the screen and scrolls inside the content region, and the shell's header and bars stay as the shell defines them. The header, the cart bar and the tab bar are the shell's, so their actions are not repeated here, except the cart bar's one action, which opens the Cart and is listed under Actions.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Categories | static | text, as the page title | Always |
  | Category image | [[domain:entities/category]] `image` | image, inside the card's colored box | One card per category, when the category has an image; otherwise the box is plain |
  | Category name | [[domain:entities/category]] `name` | text, as a link beneath the box | One card per category |

- **Input rules** — None. The employee fills in nothing on this screen; they only tap a category's name.
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Beverages | nav | The categories have loaded | The name link in the [[design:components/sundal/employee-app/category-card]] opens that category's items | [[design:surfaces/sundal/employee-app/record-a-purchase#category-items-list]] |
  | Tea and coffee | nav | The categories have loaded | The name link in the [[design:components/sundal/employee-app/category-card]] opens that category's items | [[design:surfaces/sundal/employee-app/record-a-purchase#category-items-list]] |
  | Cake | nav | The categories have loaded | The name link in the [[design:components/sundal/employee-app/category-card]] opens that category's items | [[design:surfaces/sundal/employee-app/record-a-purchase#category-items-list]] |
  | Biscuits | nav | The categories have loaded | The name link in the [[design:components/sundal/employee-app/category-card]] opens that category's items | [[design:surfaces/sundal/employee-app/record-a-purchase#category-items-list]] |
  | Sweets | nav | The categories have loaded | The name link in the [[design:components/sundal/employee-app/category-card]] opens that category's items | [[design:surfaces/sundal/employee-app/record-a-purchase#category-items-list]] |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The categories failed to load, or the phone is offline | Asks the server for the categories again and shows the loading state | — |
  | View cart | nav | The cart holds at least one item | The shell's [[design:components/sundal/employee-app/cart-bar]] opens the Cart. | [[design:surfaces/sundal/employee-app/record-a-purchase#cart-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads. The category card's placeholder state shows while the categories arrive. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the vendor has added no categories. The [[design:components/sundal/employee-app/message-block]] fills the content region. Its title reads "No snacks listed yet" and its body reads "The vendor has not added any snacks. Check again later." The employee has no action to take, so none is offered. The cart bar appears when the cart already holds items from an earlier visit. A cleared list and no results cannot occur, because the employee cannot clear categories or search them.
  - **Error** — Two errors occur. When the server cannot return the categories, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens or on Retry, the message block shows "You're offline" with Retry, and nothing changes on the server. When the employee taps the cart bar while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the tap. When the phone goes offline while the list is on screen, the [[design:components/sundal/employee-app/toast]] says "You're offline" and nothing else on screen changes. Both rules are the employee app's offline behavior in [[product:modules/sundal/employee-app]].
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
  | Ideal | Cart | The employee taps the cart bar | The screen gives way to the Cart |
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
- **Layout intent** — A page, because the employee moves into it from Categories and leaves it with Back, and it holds a list that scrolls. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the category's name as the page title and the Back control, the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]. The cart bar appears once the cart holds an item. The content is a grid of two columns, one [[design:components/sundal/employee-app/item-card]] per item, each a tall card with the photo on top and the control overlapping the photo's bottom-right edge. The eye meets the page title first, then the first row of photos. The grid scrolls inside the content region. The header, the cart bar and the tab bar are the shell's, so their actions are not repeated here, except the cart bar's one action, which opens the Cart and is listed under Actions.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Category name | [[domain:entities/category]] `name` | text, as the page title | Always |
  | Item image | [[domain:entities/item]] `image` | image, across the top of the card | One card per item |
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
  | Back | nav | Always | The [[design:components/sundal/employee-app/page-header]]'s Back control returns to the Categories list. | [[design:surfaces/sundal/employee-app/record-a-purchase#categories-list]] |
  | View cart | nav | The cart holds at least one item | The shell's [[design:components/sundal/employee-app/cart-bar]] opens the Cart. | [[design:surfaces/sundal/employee-app/record-a-purchase#cart-list]] |

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
- **Layout intent** — A page, because the employee opens it from the cart bar, and checking a list and its total takes the whole screen. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the title "Cart", and the [[design:components/sundal/employee-app/tab-bar]]. The [[design:components/sundal/employee-app/cart-bar]] is hidden here, since this screen is the cart. The content is one column with the cart's lines first, then the total in a [[design:components/sundal/employee-app/detail-card]], so the employee reads down to the commitment. Each line is a [[design:components/sundal/employee-app/cart-line]]: the item's photo at its start, then the item's name, with the [[design:components/sundal/employee-app/quantity-stepper]] at its end and the price under the stepper, so the employee recognizes each snack they added. The eye meets the page title first, then the first line, and last the total and Record purchase, which is the only primary action. Record purchase is a full-width [[design:components/sundal/employee-app/button]] in an [[design:components/sundal/employee-app/action-bar]] fixed to the bottom of the screen, directly above the tab bar, in the place the cart bar has on the other screens. The content scrolls above the bar and ends clear of it. A [[design:components/sundal/employee-app/line-notice]] about a line appears directly under that line. The list scrolls inside the content region.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Cart | static | text, as the page title | Always |
  | Item image | [[domain:entities/item]] `image` | image, at the start of the line, as a rounded square | One line per item in the cart |
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
  | Record purchase | primary | The cart holds at least one item | A primary [[design:components/sundal/employee-app/button]]. Shows "Recording…" and blocks a second tap while the server saves. If a price, an item or the stock changed, or the save fails, the employee stays here with the error state below and nothing is recorded. | [[design:surfaces/sundal/employee-app/record-a-purchase#purchase-detail-detail]] |
  | + | secondary | The cart holds fewer of the item than are available | Raises the quantity by one per tap. The line and the total update once the server confirms. | — |
  | − | secondary | The line is in the cart | Lowers the quantity by one per tap. From 1, the line is removed. The total updates once the server confirms. | — |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The cart failed to load, the phone is offline, or a step failed | Repeats the step that failed | — |
  | Browse snacks | nav | The cart is empty | A [[design:components/sundal/employee-app/button]]. Opens the categories | [[design:surfaces/sundal/employee-app/record-a-purchase#categories-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads, because the cart is kept on the employee's account. Placeholder lines in the shape of the cart lines show while it arrives. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the employee took the last item out with −. First use cannot occur, because the cart bar that opens this screen is hidden while the cart is empty. The message block fills the content region. Its title reads "Your cart is empty" and its body reads "Add snacks from the shop to record a purchase." Browse snacks sits below it.
  - **Error** — Five errors occur. When the cart cannot load, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the employee taps +, − or Record purchase while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the same step. When the server cannot save the purchase, the screen shows the E5 message from the flow, nothing is recorded, and the cart stays as it was, so the employee taps Record purchase again. When a price, an item or the stock changed while the cart was open (E4), a line notice appears under that line, the quantity is lowered, and nothing is recorded until the employee taps Record purchase again. The notice reads "The price changed. Check the total." for a changed price, "Not enough of this snack is available. The quantity was lowered." for short stock, and "This snack is no longer available." for a removed item, which the employee takes out with −. No notice shows the stock number. When the phone goes offline while the cart is on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — A cart with one line shows that line, with a total equal to its price times its quantity, and Record purchase below. The cart still shows the ideal layout. An image that is missing or fails to load shows the item card's plain tile.
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

- **Accessibility** — The page title is the first heading. The lines follow in reading order, then the total, Record purchase and the tab bar, which is also the focus order. Each line is a group named for its item. The image carries empty alternative text, because the name already says what it shows. The quantity stepper's accessibility contract applies, in [[design:components/sundal/employee-app/quantity-stepper]]. Record purchase follows the button's accessibility contract. The total is read before Record purchase. The line notice follows its own contract. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

### Purchase detail (detail)

The employee sees one recorded purchase: what they took, what it cost and when it was recorded.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] purchase-detail
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] review-and-record, look-back
- **Flow steps** — [[product:flows/sundal/employee-app/purchase-log]] S4; [[product:flows/sundal/employee-app/record-a-purchase]] S8
- **Layout patterns** — [[design:layout-patterns/employee-app-shell]]
- **Layout intent** — A page, because it is the whole outcome of recording and the whole of one purchase when the employee opens it later. It sits under the Logs tab, so Logs is the selected tab, whether the employee arrives from recording or from the Logs list. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the title "Purchase" and, only when the employee opened the purchase from the Logs list, the Back control; after recording, the header holds the title alone and the employee leaves by the tab bar. The shell also supplies the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]. The cart bar shows only when the cart holds items, as it does on every tab, and tapping it opens the Cart. The content runs top to bottom on the white page color: a confirmation message when the employee has just recorded the purchase, then a white card headed "3 items in this purchase" with one [[design:components/sundal/employee-app/purchase-line]] for each entry, then a [[design:components/sundal/employee-app/detail-card]] with the item count and the total, then a [[design:components/sundal/employee-app/detail-card]] titled "Purchase details" with the time the purchase was recorded. A line shows the item's photo, its name, its price and quantity beneath, and the line's total on the right. The eye meets the confirmation first when it shows, and otherwise the heading. The totals come after the lines and stand apart from them. The screen holds nothing to change: an employee cannot cancel an entry, so it offers no cancel, edit or void action. The content scrolls inside the content region.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Purchase | static | text, as the page title | Always |
  | Confirmation | system: the employee has just recorded this purchase | text reading "Your purchase has been recorded" | Only when the employee arrives from recording |
  | Items heading | derived from [[product:entities/sundal/entry]] `item` — the number of entries in the purchase | text, such as "3 items in this purchase" | Always |
  | Item image | [[domain:entities/item]] `image` | image, a rounded square at the start of the line | One line for each entry |
  | Item name | [[product:entities/sundal/entry]] `item` | text | One line for each entry |
  | Price and quantity | [[product:entities/sundal/entry]] `price` | text under the name, such as "₹20 x 2": the price of one item as shown when the purchase was recorded, then the entry's quantity | One line for each entry |
  | Line total | derived from [[product:entities/sundal/entry]] `price` — the price times the entry's quantity | money, in rupees, in bold at the end of the line | One line for each entry |
  | Items | derived from [[product:entities/sundal/entry]] `item` — the number of entries | number, in the totals card | Always |
  | Total | [[domain:entities/purchase]] `total` | money, in rupees, in bold under a rule in the totals card | Always |
  | Recorded on | [[domain:entities/purchase]] `time` | date and time, in Indian time, such as Wed, 18 Nov 2026, 3:42 pm, in a card titled "Purchase details" | Always |

- **Input rules** — None. The screen holds no input.
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The purchase failed to load, or the phone is offline | Asks the server for the purchase again and shows the loading state | — |
  | Back | nav | The employee opened the purchase from the Logs list | The [[design:components/sundal/employee-app/page-header]]'s Back control returns to the Logs list. | back |
  | View cart | nav | The cart holds at least one item | The shell's [[design:components/sundal/employee-app/cart-bar]] opens the Cart. | [[design:surfaces/sundal/employee-app/record-a-purchase#cart-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads. Placeholder lines in the shape of the entry lines show while the purchase arrives. The header and the tab bar are already in view.
  - **Empty** — None. A purchase holds at least one entry, because a cart needs at least one item to be recorded.
  - **Error** — Two errors occur. When the server cannot return the purchase, the message block fills the content region with Retry below it. When the employee has just recorded the purchase, it reads "Your purchase was recorded, but it could not be shown. Try again." and says nothing is lost, so the employee does not record it twice. When the employee opened the purchase from Logs, it reads "Something went wrong. Try again." When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the employee taps the cart bar while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the tap. When the phone goes offline while the purchase is on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — A purchase with one entry shows one line, and the total equals that line's price times its quantity.
  - **Access-gated** — None. An employee reaches only their own purchases, so no other employee's purchase is ever shown.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The purchase arrives | The confirmation, the lines and the cards replace the placeholder lines |
  | Loading | Error | The server cannot return the purchase, or the phone is offline | The error message and Retry replace the placeholder lines |
  | Error | Loading | The employee taps Retry | The error message gives way to the placeholder lines |
  | Ideal | Cart | The employee taps the cart bar | The screen gives way to the Cart |
  | Ideal | Ideal | The phone goes offline | A toast says "You're offline", and the screen stays as it is |

- **Accessibility** — The page title is the first heading. The confirmation is announced once as the screen opens. The time, the lines and the total follow in reading order, then the cart bar and the tab bar, which is also the focus order. Each line is read as the item's name, its price, the quantity and the line's total. The totals card is read after the last line, and the card titled "Purchase details" after that. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. The surface is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Each card shows a colored box, a different color for each category, with the category's name as a link beneath it and no item count | proposed | |
| The Categories actions list one row for each of the five sample categories the design shows, so each card links in a prototype. The vendor's real categories open their items the same way. | proposed | |
| The categories are a grid of two columns of cards | proposed | |
| The empty message reads "No snacks listed yet" with the body "The vendor has not added any snacks. Check again later." | proposed | |
| A failed load uses "Something went wrong" with the body "Try again." | proposed | |
| The items are a grid of two columns of tall cards, with the photo on top and the control overlapping the photo's bottom-right edge, after the product cards of Blinkit, Zepto and Instamart | proposed | |
| Prices show in rupees | proposed | |
| An out-of-stock card shows "Out of stock" in place of Add, at full contrast | proposed | |
| An empty category reads "No snacks in this category yet" with the body "The vendor has not added any snacks here. Try another category." | proposed | |
| The Cart shows the lines, then the total, and Record purchase sits in a bar fixed above the tab bar, so it is always in reach | proposed | |
| The cart bar is hidden on the Cart screen, since the screen is the cart | proposed | |
| The cart has no clear-all action: the employee takes each item out with − | proposed | |
| Each cart line shows the item image, matching the card the employee added the item from | proposed | |
| The notices under a line read "The price changed. Check the total.", "Not enough of this snack is available. The quantity was lowered." and "This snack is no longer available." | proposed | |
| An empty cart reads "Your cart is empty" with the body "Add snacks from the shop to record a purchase." and a Browse snacks action | proposed | |
| The cart bar shows on Purchase detail when the cart holds items, as it does on every tab | proposed | |
| The confirmation "Your purchase has been recorded" shows only when the employee arrives from recording, not when they open the purchase from Logs | proposed | |
| Purchase detail shows the time in Indian time, such as 17 Nov 2026, 3:42 pm | proposed | |
| When Purchase detail cannot load after recording, the message says the purchase was recorded, so the employee does not record it twice | proposed | |
| Purchase detail has no cancel, edit or void action | proposed | |
| Purchase detail shows the lines in a card, the totals in a second card and the time in a third, on the white page color, after the order summary of Blinkit, Zepto and Instamart, without its fees, discounts, payment, address, order id and help link | proposed | |
| Each line shows the price and quantity under the name and the line's total on the right | proposed | |
| Back shows on Purchase detail only when the employee opened the purchase from the Logs list. After recording, the header holds the title alone and the employee leaves by the tab bar. | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| In what order are the categories listed: the order the vendor created them in, or alphabetical? | Shivani Erlewad | The vendor's catalog screens are designed |
| Is a category image required when the vendor creates a category, and what shape and size does it take? | Shivani Erlewad | The vendor's catalog screens are designed |
| The design system and its Voice and tone are not recorded. Do these messages follow a voice the system sets? | Shivani Erlewad | The design system page exists |
| In what order are the items listed within a category? | Shivani Erlewad | The vendor's catalog screens are designed |
| The flow describes changing a quantity with − only in the cart (A1). Does − on the items screen also remove an item at 1? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| How does the employee leave the Cart? The shell puts Back on Items, and on Purchase when it is opened from Logs, so the Cart has the tab bar alone. | Shivani Erlewad | The shell's header is settled |
| The overview says an employee can empty the cart. Is a clear-all action needed beyond − on each item? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| What shape and size is the item image on a cart line? The item card asks the same question. | Shivani Erlewad | The design system page exists |
| How does a line show when the vendor has voided its entry? The Entry entity has no void state yet. | Shivani Erlewad | The vendor's void screens are designed |
| What does the employee do after recording: does Purchase detail offer a way to record another purchase, or do they leave by the tab bar? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |

## Related

- [[components/sundal/employee-app/action-bar]] — the bar that holds Record purchase at the bottom of the Cart screen.
- [[components/sundal/employee-app/button]] — the control for Retry.
- [[components/sundal/employee-app/cart-bar]] — the bar that shows the cart's count and total and opens the Cart.
- [[components/sundal/employee-app/cart-line]] — the line each item in the cart shows as.
- [[components/sundal/employee-app/category-card]] — the card each category shows as.
- [[components/sundal/employee-app/detail-card]] — the card that shows the purchase's totals and the time it was recorded.
- [[components/sundal/employee-app/item-card]] — the card each item shows as.
- [[components/sundal/employee-app/line-notice]] — the message under a card about that item.
- [[components/sundal/employee-app/message-block]] — the block that fills the content region with an empty, error or offline message.
- [[components/sundal/employee-app/page-header]] — the header that shows the page title.
- [[components/sundal/employee-app/purchase-line]] — the line each item of a recorded purchase shows as.
- [[components/sundal/employee-app/quantity-stepper]] — the control that changes an item's quantity.
- [[components/sundal/employee-app/screen]] — the frame every screen sits in, which sets the page color and leaves room for the fixed bars.
- [[components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[components/sundal/employee-app/toast]] — the message that says the phone is offline.
- [[information-architecture/employee-app]] — the sitemap nodes these screens sit on.
- [[journeys/employee-record-a-purchase]] — the journey whose stages these screens serve.
- [[layout-patterns/employee-app-shell]] — the frame these screens sit in.
- [[domain:entities/cart]] — the entity that holds the quantity an item has in the cart.
- [[domain:entities/category]] — the entity whose name and image each category card shows.
- [[domain:entities/item]] — the entity whose image, name, description and price each item card shows.
- [[domain:entities/purchase]] — the entity whose time and total the purchase shows.
- [[product:entities/sundal/entry]] — the entity whose item, quantity and price each line of a purchase shows.
- [[product:features/sundal/employee-app/record-a-purchase]] — the feature these screens realize.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the flow whose steps happen on these screens.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screens.
