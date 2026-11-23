---
title: Employee app
type: information-architecture
template-version: 2
kind: application
platforms: [mobile]
includes: []
opens-on: "mobile-number"
journeys:
  - "[[design:journeys/employee-record-a-purchase]]"
layout-patterns:
  - "[[design:layout-patterns/employee-app-shell]]"
sources: []
related: ["[[product:flows/sundal/employee-app/purchase-log]]","[[product:flows/sundal/employee-app/record-a-purchase]]","[[product:flows/sundal/employee-app/sign-in]]"]
invalidates: []
created: 2026-11-17
updated: 2026-11-23
owner: design
authorship: curated
origination: originate
confidence: medium
---

## Application identity

The employee app is the phone app where an employee records purchases, looks back at them and sees their details. It serves the Employee ([[product:personas/employee]]), who works at a company the vendor serves and records only their own purchases, and holds three areas, Browse, Logs and Profile, plus the cart that the cart bar opens and the sign-in screens. Its shell is [[design:layout-patterns/employee-app-shell]].

The employee signs in with their mobile number ([[domain:entities/profile]]) and an OTP ([[domain:entities/otp]]), and the sign-in screens belong to this app. The app keeps the employee signed in between visits. The vendor app and company access are outside this map.

## Scope

The whole employee app: the sign-in screens, the categories list and the items in each category, the cart, the employee's list of purchases and each purchase's detail, and the employee's profile.

## Players, channels & contexts

**Players**
- The Employee is the primary actor. They take snacks at the shop and record them on their own phone ([[product:personas/employee]]).
- The vendor runs the shop and is busy making tea and doing other work, so purchases often go unrecorded. The app gives them a record without recording anything ([[product:prds/sundal]]).
- The company admin sees only the company's monthly total. Today they receive the bill from the employee who records a day's purchases, and they pay the vendor every month.
- Blinkit, Zepto and Instamart are design references, not competitors to this app.
- Walk-in customers come to the shop and pay in cash there, instead of using the employee app. They never use the app, and their sales are not recorded in Sundal, so the vendor's stock counts can drift from the shelf ([[product:prds/sundal]]).

**Channels**
- The app on a phone. It works online only.
- The company's own bill: one employee records a whole day's purchases from everyone and gives the bill to the company admin, who pays the vendor every month. The app is meant to replace this.

**Contexts**
- At the shop, standing, with a phone, wanting it quick.
- Away from the shop, recording later from memory, with or without a connection. The wiki does not yet record how often this happens.
- Offline. The phone can lose its connection. A toast says "You're offline". Tapping anything that needs the server shows "You're offline" with Retry ([[product:modules/sundal/employee-app]]).
- The wiki records nothing about phone sizes, network speed or how often an employee uses the app.

**Constraints the structure has to fit**
- English only, built for all of India.
- Phones only, online only, and light on data.
- Simple for non-technical users and quick to ship.
- A sole designer and no dates.
- Employees change quantity with + and − only, and never see the stock number.
- The cart bar is hidden while the cart is empty.

## Sitemap / structure

| Node | Label | Parent | Reached by | Route | Lands on | Also under | Shown to | Order | Group | Icon |
|---|---|---|---|---|---|---|---|---|---|---|
| browse | Browse | None. | global | None. | categories | None. | employee | 1 | tab-bar | None. |
| categories | Categories | browse | local | None. | None. | None. | employee | 1 | None. | None. |
| category-items | Items | categories | contextual | None. | None. | None. | employee | 1 | None. | None. |
| logs | Logs | None. | global | None. | None. | None. | employee | 2 | tab-bar | None. |
| purchase-detail | Purchase | logs | contextual | None. | None. | None. | employee | 1 | None. | None. |
| profile | Profile | None. | global | None. | None. | None. | employee | 3 | tab-bar | None. |
| cart | Cart | None. | utility | None. | None. | None. | employee | 4 | None. | None. |
| mobile-number | Mobile number | None. | global | None. | None. | None. | employee | 5 | None. | None. |
| otp | OTP | mobile-number | contextual | None. | None. | None. | employee | 1 | None. | None. |

## Structures considered

**A. Three bottom tabs, Browse, Logs and Profile (chosen).** Browse opens on Categories, then Category items. Logs lists purchases, then Purchase detail. The cart opens from the cart bar, which sits above the tab bar. The pattern is hierarchical and shallow, with global navigation. It classifies by task: shop, review, account. Each screen belongs to one tab, so the grouping is exact. The cost is that the cart has no tab of its own and is reachable only while it holds items.

**B. No tab bar.** Home is the categories list, with Logs and Profile as icons in the top bar. The pattern is hierarchical, with utility navigation, and classifies by the same tasks. The cost is that Logs and Profile are less visible, and the employee must find the icons.

**C. One flat list of all items, with category chips across the top.** The pattern is heterarchical. It classifies by item name, with category as a filter, so the classification is ambiguous. The cost is that it contradicts the feature, where a category opens to its items, and the list grows long.

A won because it matches the designer's decision, keeps the cart-bar rule intact so the feature, the module and the task flow need no change, and gives each task one tab that stays in view, which suits an employee who wants it quick, at the shop or elsewhere.

## Navigation model

The app has four navigation systems.

- **Global.** A bottom tab bar with Browse, Logs and Profile. It is the top tier, and it is reached from every page. It gives each of the employee's three tasks, shopping, checking past purchases and their own details, one tab that stays in view. A tab does not remember where the employee was: choosing Browse always shows the Categories list.
- **Local.** Inside Browse, the Categories list shows the categories, and opening one shows its items.
- **Contextual.** Links inside a page's own content: a category opens its items, and a purchase in Logs opens its detail. Recording a purchase also lands on that purchase's detail.
- **Utility.** The cart bar. It is a secondary tool that applies across the app. It shows on Browse, Logs and Profile while the cart holds items, and it opens the Cart.

Where each system sits on a page, at each width class, is the layout pattern's navigation placement: [[design:layout-patterns/employee-app-shell]].

Sign-in is a sequence: the mobile number screen, then the OTP screen, then the Categories list. The sign-in screens show no tab bar and no cart bar.

## Taxonomy & labeling

The labels fall into three groups. The three tab labels, Browse, Logs and Profile, name where the employee is in the app. The four labels Categories, Items, Cart and Purchase name things in the shop. The two sign-in labels, Mobile number and OTP, name what the employee enters. Each one is a glossary concept.

| Label | Concept | Not to use |
|---|---|---|
| Browse | [[domain:entities/catalog]] | None. |
| Categories | [[domain:entities/category]] | None. |
| Items | [[domain:entities/item]] | Products. The reference apps use it, but the shop sells snacks it lists as items. |
| Logs | [[product:entities/sundal/purchase-log]] | History, since the employee's list is called a purchase log. |
| Purchase | [[domain:entities/purchase]] | Order, because Sundal has no payment or delivery. Entry, which is one snack line of a purchase. |
| Cart | [[domain:entities/cart]] | None. |
| Profile | [[domain:entities/profile]] | None. |
| Mobile number | [[domain:entities/profile]] | None. |
| OTP | [[domain:entities/otp]] | None. |

## URL / routing scheme

None. The app is mobile and has no addressable routes, so every Route cell in the sitemap reads "None.".

## Wayfinding

- **You are here.** Every page shows its title, and the tab it belongs to is the selected one in the tab bar. Category items shows the category's name as its title, and Purchase shows its own title.
- **Going back.** Below the tabs, Category items, and Purchase when it is opened from Logs, each have a Back control that returns to the page above, in place of breadcrumbs. After recording, Purchase has no Back and the employee leaves by the tab bar. Breadcrumbs would take space a phone doesn't have, and the structure is only two levels deep.
- **Landing.** A signed-in employee opening the app sees the Categories list, with the Browse tab selected. A signed-out employee sees the mobile number screen, and lands on Categories after the OTP.
- **Empty states point to the next step.** An empty catalog shows the empty message from the task flow (E1). An empty Logs list points the employee to Browse to record a first purchase.
- **Errors and recovery.** Offline shows "You're offline" with Retry. A failed save shows "Something went wrong. Try again." Both are in [[product:modules/sundal/employee-app]] and [[product:flows/sundal/employee-app/record-a-purchase]].

## Decisions

| Decision | State | Decided |
|---|---|---|
| Structure A (three bottom tabs, shallow hierarchy) over B (top-bar icons) and C (flat list) | adopted | Designer sign-off, 2026-11-17 |
| The categories list is the home screen: Browse lands on Categories | adopted | Designer sign-off, 2026-11-17 |
| The tab bar holds Browse, Logs and Profile, with no Cart tab and no Settings | adopted | Designer sign-off, 2026-11-17 |
| The tab is labeled "Logs" | adopted | Designer sign-off, 2026-11-17 |
| The cart opens from the cart bar, which shows on all three tabs while the cart has items | adopted | Designer sign-off, 2026-11-17 |
| A tab does not remember where the employee was | adopted | Designer sign-off, 2026-11-17 |
| Profile shows picture, name and mobile number, read only, and Log out | adopted | Designer sign-off, 2026-11-17 |
| Sign-in has two screens, mobile number then OTP | adopted | Designer sign-off, 2026-11-17 |
| The sign-in screens show no tab bar and no cart bar | adopted | Designer sign-off, 2026-11-17 |
| The app keeps the employee signed in between visits | adopted | Designer sign-off, 2026-11-17 |
| An employee on a new phone signs in with their mobile number and an OTP, as in any sign-in | adopted | Designer sign-off, 2026-11-17 |
| Purchase detail sits under Logs only. Landing on it after recording is a flow step, not a second parent. | proposed | |
| Cart is a root node reached by utility navigation | proposed | |
| The cart bar shows on Purchase detail while the cart holds items, and is hidden on the Cart, which is the cart | proposed | |
| A Back control replaces breadcrumbs | proposed | |
| The tabs use a grid for Browse, a receipt for Logs and a person for Profile, filled when selected and an outline otherwise | proposed | |
| An empty Logs list points the employee to Browse | proposed | |
| A signed-out employee opens on the mobile number screen | proposed | |
| Log out ends the saved sign-in | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Can employees find a past purchase and an item in this structure? | Shivani Erlewad | A tree test of the structure has been run |
| Do Browse, Logs and Profile read clearly as tab labels? | Shivani Erlewad | A click test on a prototype has been run |
| Does the app need an icon catalog beyond the three tab icons, and which icon set does it draw from? | Shivani Erlewad | The icon catalog exists |
| Should "Log out" read "Sign out", given "Logs" and the wiki's "sign-in"? | Shivani Erlewad | The glossary gets an entry for the action |
| Does the app need search? | Shivani Erlewad | The vendor's catalog size is known |
| Does Logs list the newest purchase first, and how does a purchase with a voided entry show? | Shivani Erlewad | Employees have been asked how they look for a purchase, and the vendor's void screens are designed |

## Related

- [[domain:entities/cart]] — the concept behind the Cart label.
- [[domain:entities/catalog]] — the concept behind the Browse label.
- [[domain:entities/category]] — the concept behind the Categories label.
- [[domain:entities/item]] — the concept behind the Items label.
- [[domain:entities/profile]] — the concept behind the Profile and Mobile number labels.
- [[domain:entities/purchase]] — the concept behind the Purchase label.
- [[product:catalogs/roles]] — the roles the sitemap's "Shown to" column names.
- [[product:entities/sundal/purchase-log]] — the concept behind the Logs label.
- [[product:flows/sundal/employee-app/purchase-log]] — the task flow an employee follows from the Logs tab to a past purchase.
- [[product:flows/sundal/employee-app/record-a-purchase]] — the task flow the structure supports.
- [[product:flows/sundal/employee-app/sign-in]] — the task flow through the mobile number and OTP screens.
- [[product:modules/sundal/employee-app]] — the module this map organizes.
- [[product:personas/employee]] — the actor it serves.
