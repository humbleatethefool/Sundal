---
title: Categories
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/record-a-purchase]]"
flows:
  - "[[product:flows/sundal/employee-app/record-a-purchase]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/cart-bar]]", "[[components/sundal/employee-app/category-card]]", "[[components/sundal/employee-app/message-block]]", "[[components/sundal/employee-app/page-header]]", "[[components/sundal/employee-app/tab-bar]]", "[[components/sundal/employee-app/toast]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/category-items]]", "[[domain:entities/category]]", "[[product:features/sundal/employee-app/record-a-purchase]]", "[[product:flows/sundal/employee-app/record-a-purchase]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee scans the vendor's categories on the Categories screen and opens the one that holds the snack they took.

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
  | Category image | [[domain:entities/category]] `image` | image, on the top of the card | One card per category |
  | Category name | [[domain:entities/category]] `name` | text, beneath the image | One card per category |

- **Input rules** — None. The employee fills in nothing on this screen; they only tap a card.
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | [[design:components/sundal/employee-app/category-card]], labeled with the category's name | nav | The categories have loaded | Opens that category's items | [[design:surfaces/sundal/employee-app/category-items#category-items-list]] |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The categories failed to load, or the phone is offline | Asks the server for the categories again and shows the loading state | — |
  | View cart, in the shell's [[design:components/sundal/employee-app/cart-bar]] | nav | The cart holds at least one item | Opens the Cart. | [[design:surfaces/sundal/employee-app/cart#cart-list]] |

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

## Platform variations

None. The surface is shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Each card shows the category's image above its name, with no item count | proposed | |
| The categories are a grid of two columns of cards | proposed | |
| The empty message reads "No snacks listed yet" with the body "The vendor has not added any snacks. Check again later." | proposed | |
| A failed load uses "Something went wrong" with the body "Try again." | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| In what order are the categories listed: the order the vendor created them in, or alphabetical? | Shivani Erlewad | The vendor's catalog screens are designed |
| Is a category image required when the vendor creates a category, and what shape and size does it take? | Shivani Erlewad | The vendor's catalog screens are designed |
| The design system and its Voice and tone are not recorded. Do these messages follow a voice the system sets? | Shivani Erlewad | The design system page exists |
| Do the cart bar and the tab bar stay in view while the list scrolls? | Shivani Erlewad | The shell's open question on this is settled |

## Related

- [[components/sundal/employee-app/button]] — the control for Retry.
- [[components/sundal/employee-app/cart-bar]] — the bar that shows the cart's count and total and opens the Cart.
- [[components/sundal/employee-app/category-card]] — the card each category shows as.
- [[components/sundal/employee-app/message-block]] — the block that fills the content region with an empty, error or offline message.
- [[components/sundal/employee-app/page-header]] — the header that shows the page title.
- [[components/sundal/employee-app/tab-bar]] — the bar that moves between Browse, Logs and Profile.
- [[components/sundal/employee-app/toast]] — the message that says the phone is offline.
- [[information-architecture/employee-app]] — the sitemap node this surface sits on.
- [[journeys/employee-record-a-purchase]] — the journey whose choose-snacks stage this surface serves.
- [[layout-patterns/employee-app-shell]] — the frame this surface sits in.
- [[surfaces/sundal/employee-app/category-items]] — the surface a category card opens.
- [[domain:entities/category]] — the entity whose name and image each category card shows.
- [[product:features/sundal/employee-app/record-a-purchase]] — the feature this surface realizes.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the flow whose steps happen here.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screen.
