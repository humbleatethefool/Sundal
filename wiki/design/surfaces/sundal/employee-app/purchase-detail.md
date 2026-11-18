---
title: Purchase detail
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/record-a-purchase]]"
flows:
  - "[[product:flows/sundal/employee-app/record-a-purchase]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/tab-bar]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[domain:entities/entry]]", "[[domain:entities/purchase]]", "[[product:features/sundal/employee-app/record-a-purchase]]", "[[product:flows/sundal/employee-app/record-a-purchase]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee sees one recorded purchase on the Purchase detail screen: what they took, what it cost and when it was recorded.

## Platform scope

Mobile only, in one layout for the compact width class, with no per-platform deltas.

## Surfaces

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
- **Layout intent** — A page, because it is the whole outcome of recording and the whole of one purchase when the employee opens it later. It sits under the Logs tab, so Logs is the selected tab, whether the employee arrives from recording or from the Logs list. The shell supplies the [[design:components/sundal/employee-app/page-header]], which carries the title "Purchase" and the Back control, the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]]. The cart bar shows only when the cart holds items, as it does on every tab, and tapping it opens the Cart. The content runs top to bottom: a confirmation message when the employee has just recorded the purchase, then the time the purchase was recorded, then one line for each entry, then the total. A line shows the item's name, the quantity and the price. The eye meets the confirmation first when it shows, and otherwise the time. The total comes last and stands apart from the lines. The screen holds nothing to change: an employee cannot cancel an entry, so it offers no cancel, edit or void action. The list scrolls inside the content region.
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
  | View cart, in the shell's [[design:components/sundal/employee-app/cart-bar]] | nav | The cart holds at least one item | Opens the Cart. | [[design:surfaces/sundal/employee-app/cart#cart-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads. Placeholder lines in the shape of the entry lines show while the purchase arrives. The header and the tab bar are already in view.
  - **Empty** — None. A purchase holds at least one entry, because a cart needs at least one item to be recorded.
  - **Error** — Two errors occur. When the server cannot return the purchase, the message block fills the content region with Retry below it. When the employee has just recorded the purchase, it reads "Your purchase was recorded, but it could not be shown. Try again." and says nothing is lost, so the employee does not record it twice. When the employee opened the purchase from Logs, it reads "Something went wrong. Try again." When the phone is offline as the screen opens, the message block shows "You're offline" with Retry. When the employee taps the cart bar while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the tap. When the phone goes offline while the purchase is on screen, the toast says "You're offline" and nothing else on screen changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — A purchase with one entry shows one line, and the total equals that line's price times its quantity.
  - **Access-gated** — None. An employee reaches only their own purchases, so no other employee's purchase is ever shown.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The purchase arrives | The confirmation, the time, the lines and the total replace the placeholder lines |
  | Loading | Error | The server cannot return the purchase, or the phone is offline | The error message and Retry replace the placeholder lines |
  | Error | Loading | The employee taps Retry | The error message gives way to the placeholder lines |
  | Ideal | Cart | The employee taps the cart bar | The screen gives way to the Cart |
  | Ideal | Ideal | The phone goes offline | A toast says "You're offline", and the screen stays as it is |

- **Accessibility** — The page title is the first heading. The confirmation is announced once as the screen opens. The time, the lines and the total follow in reading order, then the cart bar and the tab bar, which is also the focus order. Each line is read as the item's name, the quantity and the price. The total is read after the last line. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. The surface is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| A failed load uses "Something went wrong" with the body "Try again." | proposed | |
| Prices show in rupees | proposed | |
| The cart bar shows on Purchase detail when the cart holds items, as it does on every tab | proposed | |
| The confirmation "Your purchase has been recorded" shows only when the employee arrives from recording, not when they open the purchase from Logs | proposed | |
| Purchase detail shows the time in Indian time, such as 17 Nov 2026, 3:42 pm | proposed | |
| When Purchase detail cannot load after recording, the message says the purchase was recorded, so the employee does not record it twice | proposed | |
| Purchase detail has no cancel, edit or void action | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| How does a line show when the vendor has voided its entry? The Entry entity has no void state yet. | Shivani Erlewad | The vendor's void screens are designed |
| What does the employee do after recording: does Purchase detail offer a way to record another purchase, or do they leave by the tab bar? | Shivani Erlewad | The record-a-purchase flow has been tested with employees |
| The design system and its Voice and tone are not recorded. Do these messages follow a voice the system sets? | Shivani Erlewad | The design system page exists |
| Do the cart bar and the tab bar stay in view while the list scrolls? | Shivani Erlewad | The shell's open question on this is settled |

## Related

- [[components/sundal/employee-app/button]] — the control for Retry.
- [[components/sundal/employee-app/cart-bar]] — the bar that shows when the cart holds items.
- [[components/sundal/employee-app/page-header]] — the header that shows the title Purchase and Back.
- [[components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[information-architecture/employee-app]] — the sitemap node this surface sits on.
- [[journeys/employee-record-a-purchase]] — the journey whose review-and-record and look-back stages this surface serves.
- [[layout-patterns/employee-app-shell]] — the frame this surface sits in.
- [[domain:entities/entry]] — the entity whose item, quantity and price each line of a purchase shows.
- [[domain:entities/purchase]] — the entity whose time and total the purchase shows.
- [[product:features/sundal/employee-app/record-a-purchase]] — the feature this surface realizes.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the flow whose steps happen here.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screen.
