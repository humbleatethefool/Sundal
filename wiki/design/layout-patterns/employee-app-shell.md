---
title: Employee app shell
type: layout-pattern
template-version: 1
realizes:
  - "[[product:app-base]]"
platforms: [mobile]
kinds: [list, detail]
sources: []
related: []
created: 2026-11-17
updated: 2026-11-17
owner: design
authorship: curated
origination: originate
confidence: medium
---

## Purpose & usage

The employee app shell is the arrangement every employee-app page sits in: a header, the page's content, a cart bar and a tab bar. Every screen after sign-in follows it. The sign-in screens show no tab bar and no cart bar. It does not describe the contents of a screen, which each surface page does.

## Regions

| Id | Region | Role | Landmark |
|---|---|---|---|
| header | Header | The page title, and a Back control on Items and Purchase | `banner` |
| content | Content | The screen's own content | `main` |
| cart-bar | Cart bar | The item count and total, and a way into the Cart. Hidden while the cart is empty. | `region`, labeled "Cart" |
| tab-bar | Tab bar | The Browse, Logs and Profile tabs | `navigation`, labeled "Main" |

## Hierarchy

The eye meets the page title first, at the top. The content comes second and takes most of the screen. The cart bar comes third, because its total matters when the cart has items. The tab bar comes last, at the bottom. Order and grouping make this, not size or color.

## Responsive arrangement

- **Compact** — the phone. Header at the top, content in a single column, the cart bar and then the tab bar stacked at the bottom.

Only the compact width class is designed, because the app is phones only.

## Navigation placement

| Navigation system | Width class | Region | Form |
|---|---|---|---|
| global | compact | tab-bar | bottom bar |
| utility | compact | cart-bar | bar above the tab bar |
| local | compact | content | list |
| contextual | compact | content | links in the content |

## Components placed

- [[design:components/sundal/employee-app/cart-bar]] — in the cart-bar region.
- [[design:components/sundal/employee-app/page-header]] — in the header region.
- [[design:components/sundal/employee-app/tab-bar]] — in the tab-bar region.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The tab bar sits at the bottom | adopted | Designer sign-off, 2026-11-17 |
| The cart bar sits directly above the tab bar | proposed | |
| The Back control sits in the header | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Do the cart bar and tab bar stay in view while the content scrolls? | Shivani Erlewad | The surface pages are written |
| Is a wider phone or landscape layout needed? | Shivani Erlewad | A test shows employees using it |

## Related

None.

