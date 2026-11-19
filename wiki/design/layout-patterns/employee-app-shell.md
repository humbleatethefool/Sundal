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

The employee app shell is what every employee-app page sits in: a header, the content, a cart bar and a tab bar. Every screen after sign-in follows it. The sign-in screens show no tab bar and no cart bar. It does not describe the contents of a screen, which each surface page does.

## Regions

| Id | Region | Role | Landmark |
|---|---|---|---|
| header | Header | The page title, and a Back control on Items and on Purchase when it is opened from Logs | `banner` |
| content | Content | The screen's own content | `main` |
| cart-bar | Cart bar | The item count and total, and a way into the Cart. Hidden while the cart is empty. | `region`, labeled "Cart" |
| action-bar | Action bar | The screen's one main action as a full-width button, such as Record purchase on the Cart. It takes the cart bar's place and shows only on a screen with such an action. | `region`, labeled "Actions" |
| tab-bar | Tab bar | The Browse, Logs and Profile tabs, each an icon above its label, in a floating card fixed to the bottom of the screen | `navigation`, labeled "Main" |

## Hierarchy

The eye meets the page title first, at the top. The content comes second and takes most of the screen. The cart bar comes third, because its total matters when the cart has items. The tab bar comes last, at the bottom. Order and grouping make this, not size or color.

## Responsive arrangement

- **Compact** — the phone. Header at the top, content in a single column, the cart bar and then the tab bar stacked at the bottom. The cart bar and the tab bar are fixed to the screen, the cart bar directly above the tab bar, and the content scrolls above them and ends clear of both. Every block shares one side gutter, 16 px, and the blocks sit 16 px apart, so the title, the content and the fixed bars have the same left and right edge.

Only the compact width class is designed, because the app is phones only.

## Navigation placement

| Navigation system | Width class | Region | Form |
|---|---|---|---|
| global | compact | tab-bar | bottom bar |
| utility | compact | cart-bar | bar above the tab bar |
| local | compact | content | list |
| contextual | compact | content | links in the content |

## Components placed

- [[design:components/sundal/employee-app/action-bar]] — in the action-bar region.
- [[design:components/sundal/employee-app/cart-bar]] — in the cart-bar region.
- [[design:components/sundal/employee-app/page-header]] — in the header region.
- [[design:components/sundal/employee-app/screen]] — around the whole shell, setting the page color, the side gutter and the room for the fixed bars.
- [[design:components/sundal/employee-app/tab-bar]] — in the tab-bar region.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The tab bar sits at the bottom | adopted | Designer sign-off, 2026-11-17 |
| The cart bar sits directly above the tab bar | proposed | |
| The cart bar and the tab bar are fixed to the bottom of the screen while the content scrolls | proposed | |
| On the Cart screen the action bar takes the cart bar's place above the tab bar, because the screen is the cart | proposed | |
| The page is white and its blocks share a 16 px side gutter and a 16 px gap, set by the screen frame | proposed | |
| The Back control sits in the header | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Is a wider phone or landscape layout needed? | Shivani Erlewad | A test shows employees using it |

## Related

None.

