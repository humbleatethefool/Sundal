---
title: Log
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/log]]"
flows:
  - "[[product:flows/sundal/employee-app/log]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/message-block]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/tab-bar]]", "[[components/sundal/employee-app/toast]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/record-a-purchase]]", "[[domain:entities/entry]]", "[[domain:entities/log]]", "[[domain:entities/purchase]]", "[[product:features/sundal/employee-app/log]]", "[[product:flows/sundal/employee-app/log]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee scans their own recorded purchases and opens the one they want to check.

## Platform scope

Mobile only, in one layout for the compact width class, with no per-platform deltas.

## Surfaces

### Log (list)

The employee looks through the purchases they recorded and opens one. Purchase detail is not specified here: it is one screen reached from two places, and [[design:surfaces/sundal/employee-app/record-a-purchase#purchase-detail-detail]] specifies it, including the case where the employee opens it from this list.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] logs
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] look-back
- **Flow steps** — [[product:flows/sundal/employee-app/log]] S1, S2, S3, S5, E1, E2, E3, T1, T2, T3
- **Layout patterns** — [[design:layout-patterns/employee-app-shell]]
- **Layout intent** — A page, because Log is the root of the Logs tab and the employee reaches it from the tab bar at any time. The shell supplies the [[design:components/sundal/employee-app/page-header]], with the title alone and no Back, the [[design:components/sundal/employee-app/cart-bar]] and the [[design:components/sundal/employee-app/tab-bar]], with Logs selected. This screen adds what fills the content region: a single column of purchase rows, one for each purchase, newest first. Each row is the whole width of the screen and a tap target at least 44 px high. A row shows the time the purchase was recorded as its main line, the number of items beneath it in small muted text, and the purchase total in bold at the end, followed by a chevron. The eye meets the page title first and the newest row second. The rows are plain and flat so that a long list stays quick to scan. The list scrolls inside the content region, and the shell's header and bars stay as the shell defines them. A purchase row is a part this screen needs that no component page covers yet, so it is recorded as an open question.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Logs | static | text, as the page title | Always |
  | Recorded on | [[domain:entities/purchase]] `time` | date and time in Indian time, such as Wed, 18 Nov 2026, 3:42 pm, as the row's main line | One row for each purchase |
  | Items | derived from [[domain:entities/entry]] `item` — the number of entries in the purchase | text under the time, such as "3 items", and "1 item" for one | One row for each purchase |
  | Total | [[domain:entities/purchase]] `total` | money, in rupees, in bold at the end of the row | One row for each purchase |

- **Input rules** — None. The employee fills in nothing on this screen; they only tap a row.
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Purchase row, the whole row | nav | The list has loaded | Opens that purchase. Back on the opened screen returns here. | [[design:surfaces/sundal/employee-app/record-a-purchase#purchase-detail-detail]] |
  | Browse snacks, a [[design:components/sundal/employee-app/button]] | nav | The employee has recorded no purchase | Opens the Categories list on the Browse tab | [[design:surfaces/sundal/employee-app/record-a-purchase#categories-list]] |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The list failed to load, or the phone is offline | Asks the server for the list again and shows the loading state | — |
  | View cart | nav | The cart holds at least one item | The shell's [[design:components/sundal/employee-app/cart-bar]] opens the Cart. | [[design:surfaces/sundal/employee-app/record-a-purchase#cart-list]] |

- **Resilience states** —
  - **Loading** — The whole content region loads. Row-shaped placeholders show while the list arrives, in the shape of the rows. The header and the tab bar are already in view.
  - **Empty** — One version occurs: the employee has recorded no purchase ([[domain:entities/log]] is empty until the first one is confirmed). The [[design:components/sundal/employee-app/message-block]] fills the content region. Its title reads "No purchases yet" and its body reads "Add snacks from the shop to record a purchase.", with Browse snacks below it. A cleared list and no results cannot occur, because the employee cannot remove a purchase or search the list.
  - **Error** — Two errors occur. When the server cannot return the list, the message block fills the content region: title "Something went wrong" and body "Try again.", with Retry below it. When the phone is offline as the screen opens or on Retry, the message block shows "You're offline" with Retry, and nothing changes on the server. When the employee taps a row or the cart bar while the phone is offline, the screen shows "You're offline" with Retry, nothing changes on the server, and Retry repeats the tap. When the phone goes offline while the list is on screen, the [[design:components/sundal/employee-app/toast]] says "You're offline" and nothing else on screen changes. These are the employee app's offline rules in [[product:modules/sundal/employee-app]].
  - **Partial** — One purchase shows as one row at the top of the list, with nothing below it. The row opens its purchase like any other.
  - **Access-gated** — None. Only a signed-in employee reaches this screen, and each employee sees only their own purchases, so no other employee's purchase is ever listed.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Loading | Ideal | The list arrives | The rows replace the placeholder rows |
  | Loading | Empty | The server returns no purchases | The empty message replaces the placeholder rows |
  | Loading | Error | The server cannot return the list, or the phone is offline | The error message and Retry replace the placeholder rows |
  | Error | Loading | The employee taps Retry | The error message gives way to the placeholder rows |
  | Empty | Loading | The employee opens Logs again after recording a purchase | The empty message gives way to the placeholder rows, then the list |
  | Ideal | Purchase detail | The employee taps a row | The screen gives way to the purchase |
  | Ideal | Cart | The employee taps the cart bar | The screen gives way to the Cart |
  | Ideal | Ideal | The phone goes offline | A toast says "You're offline", and the screen stays as it is |

- **Accessibility** — The page title is the first heading. The rows follow in reading order, newest first, then the cart bar and the tab bar, which is also the focus order. The list is one list, and each row is one link read as the time, the number of items and the total, for example "Wed, 18 Nov 2026, 3:42 pm, 3 items, 120 rupees". The chevron is decorative. The loading state announces "Loading purchases", and the empty and error messages are announced as they appear. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. The surface is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The list shows the newest purchase first, so the one the employee just recorded or took most recently is in view | proposed | |
| A row shows the time, the number of items and the total, and nothing else, so each purchase is told apart without opening it | proposed | |
| The whole row is the tap target, and a chevron after the total shows that it opens | proposed | |
| The row shows the time in Indian time in the same format as the Purchase detail screen's "Purchase details" card | proposed | |
| The empty message reads "No purchases yet" with the body "Add snacks from the shop to record a purchase." and a Browse snacks action, the cart's empty wording being reused for the body | proposed | |
| A failed load uses "Something went wrong" with the body "Try again.", as the other screens do | proposed | |
| The list has no search, filter, grouping or cancel action | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Which component carries a purchase row? No component page covers a row that shows a time, a count and a total, and the purchase line shows one item. | Shivani Erlewad | The component spec for the row is written |
| In what order should the list read, newest first or grouped by month, since a company's purchases are totalled per month? The IA asks the order question too. | Shivani Erlewad | Employees have been asked how they look for a purchase |
| Does the list load all purchases at once, or in parts? The employee app is light on data, and the volume per employee is not recorded. | Shivani Erlewad | The volume of purchases for an employee is known |
| How does a row show a purchase that holds a voided entry: its original total, its total after the void or a mark? The Entry entity has no void state yet. | Shivani Erlewad | The vendor's void screens are designed |
| Does the list keep its place when the employee returns with Back, or start at the top? | Shivani Erlewad | A click test on a prototype has been run |
| The "Purchase details" card shows the time as "Wed, 18 Nov 2026, 3:42 pm", and the record-a-purchase surface's decisions show "17 Nov 2026, 3:42 pm". Which format do the rows use? | Shivani Erlewad | The two pages are reconciled |
| The save-failure wording in the record-a-purchase flow reads "Please try again", and the design system's voice and tone leaves out "please". This screen follows the voice and tone. | Shivani Erlewad | The two pages are reconciled |

## Related

- [[design:components/sundal/employee-app/button]] — the control for Browse snacks and Retry.
- [[design:components/sundal/employee-app/cart-bar]] — the bar that shows the cart's count and total and opens the Cart.
- [[design:components/sundal/employee-app/message-block]] — the block that fills the content region with an empty, error or offline message.
- [[design:components/sundal/employee-app/page-header]] — the header that shows the page title.
- [[design:components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[design:components/sundal/employee-app/toast]] — the message that says the phone is offline.
- [[design:information-architecture/employee-app]] — the sitemap node this screen sits on.
- [[design:journeys/employee-record-a-purchase]] — the journey whose look-back stage this screen serves.
- [[design:layout-patterns/employee-app-shell]] — the frame this screen sits in.
- [[design:surfaces/sundal/employee-app/record-a-purchase]] — the surface page that specifies the Purchase detail screen this list opens.
- [[domain:entities/entry]] — the entity whose count each row shows.
- [[domain:entities/log]] — the entity this screen lists.
- [[domain:entities/purchase]] — the entity whose time and total each row shows.
- [[product:features/sundal/employee-app/log]] — the feature this screen realizes.
- [[product:flows/sundal/employee-app/log]] — the flow whose steps happen on this screen.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screen.
