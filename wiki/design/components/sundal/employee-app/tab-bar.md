---
title: Tab bar
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:modules/sundal/employee-app]]"
sources: []
related: ["[[information-architecture/employee-app]]", "[[layout-patterns/employee-app-shell]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The tab bar is the bar at the bottom of the employee app that moves the employee between Browse, Logs and Profile. It is the app's main navigation, and it stays in view on every screen after sign-in. The selected tab tells the employee where they are.

Use it for moving between the app's areas.
- Do keep it to Browse, Logs and Profile, in that order.
- Do show it on every screen after sign-in, and not on the sign-in screens.
- Do not put the cart in it. The cart opens from the cart bar.
- Do not use it for moving within an area. Back and links in the content do that.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The bar, sitting at the bottom of the screen below the cart bar. |
| Tab | Required | One per area. Each has a label. |
| Selected indicator | Required | Marks the tab for the area the employee is in. |

## Variants

None. The bar has one configuration, with a tab for each area. Its labels are fixed words, so no content varies.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Unselected tab | The label alone. |
| Selected tab | The label with the selected indicator, which is marked by more than color. |
| Pressed | Feedback while the employee's finger is on a tab. Its form waits for the design system. |
| Focus | A visible focus indication on the tab. Its form waits for the design system. |

## Props / API

None documented yet.

## Behavior & interaction

- Tapping a tab opens that area's first screen: Browse shows the categories, Logs shows the employee's purchases and Profile shows their details.
- A tab does not remember where the employee was. Choosing Browse always shows the categories.
- The selected tab is the one for the area the current screen belongs to. A purchase's detail, whether reached from recording or from Logs, sits under Logs.
- The bar stays in place while the content scrolls, and it sits below the cart bar.
- The bar is not shown on the sign-in screens.
- No motion is specified.

## Accessibility

- The bar is a navigation landmark labeled "Main", as the shell sets out. Its tabs are read as a list.
- A screen reader announces which tab is selected.
- The selected state is shown by more than color.
- Text meets a contrast ratio of 4.5 to 1, and the selected indicator meets 3 to 1 against its background.
- Each tab is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.
- Focus runs through the tabs in order, Browse, Logs, Profile.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The labels are Browse, Logs and Profile, in sentence case, taken from the app's vocabulary on the information architecture page. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The selected tab is marked by more than color | proposed | |

The bar's placement, its tabs and the rule that a tab does not remember where the employee was are recorded on [[information-architecture/employee-app]] and [[layout-patterns/employee-app-shell]].

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the bar's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| Which icons do the tabs use, if any? | Shivani Erlewad | The icon catalog exists |
| What does tapping the tab that is already selected do? | Shivani Erlewad | A screen of the bar has been designed |
| Do Browse, Logs and Profile read clearly as tab labels? | Shivani Erlewad | A click test on a prototype has been run |

## Related

- [[information-architecture/employee-app]] — the structure whose areas the bar links, and the decisions it records.
- [[layout-patterns/employee-app-shell]] — the shell that places the bar at the bottom of every screen.
