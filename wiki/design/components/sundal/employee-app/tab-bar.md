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
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The tab bar is a floating card at the bottom of the employee app that moves between Browse, Logs and Profile. It is the app's main navigation, and it is fixed to the bottom of the screen on every screen after sign-in. The selected tab tells the employee where they are.

Use it for moving between the app's areas.
- Do keep it to Browse, Logs and Profile, in that order.
- Do show it on every screen after sign-in, and not on the sign-in screens.
- Do not put the cart in it. The cart opens from the cart bar.
- Do not use it for moving within an area. Back and links in the content do that.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | A white card with rounded corners and a soft shadow, inset from the screen's edges and fixed to the bottom of the screen, below the cart bar. |
| Tab | Required | One per area. Each has an icon above its label. |
| Selected indicator | Required | Marks the tab for the area the employee is in: a filled icon and a bold label in the dark text color. |

## Variants

None. The bar has one configuration, with a tab for each area. Its labels are fixed words, so no content varies.

## Tokens & measurements

The definition uses Bootstrap's classes and the design system's color tokens only.

| Part | Value | Token or class |
|---|---|---|
| Container fill | The card color | the project token `surface-card` |
| Container corners | Rounded | `rounded` |
| Container shadow | Soft shadow | `shadow` |
| Container inset from the screen's sides | Spacing 3 | `mx-3` |
| Container position | Fixed to the bottom of the screen | `fixed-bottom`, clear of the screen's edge by `mb-3` |
| Selected icon | The dark text color | `text-dark` |
| Selected label | Bold, dark text color | `fw-bold`, `text-dark` |
| Unselected icon and label | The muted text color, the same as every description | `text-body-secondary` |
| Label type | Small | `small` |
| Icon and label gap | Spacing 1 | `gap-1` |

The icon size and the card's inset have no fitting token, so both are recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Unselected tab | An outline icon above the label, both in a muted gray. |
| Selected tab | A filled icon above the label, which is bold, both in the dark text color. The selected tab differs by icon fill and label weight as well as color. |
| Pressed | Feedback while the employee's finger is on a tab. Its form waits for the design system. |
| Focus | A visible focus indication on the tab. Its form waits for the design system. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `browseSelected` | Boolean | `false` | Optional | Makes Browse the selected tab. |
| `logsSelected` | Boolean | `false` | Optional | Makes Logs the selected tab. |
| `profileSelected` | Boolean | `false` | Optional | Makes Profile the selected tab. |

Set one prop at a time. The labels are fixed words, so no string is a prop. The definition is `design/components/tab-bar.json`, with its markup in `design/components/tab-bar.html`.

## Behavior & interaction

- Tapping a tab opens that area's first screen: Browse shows the categories, Logs shows the employee's purchases and Profile shows their details.
- A tab does not remember where the employee was. Choosing Browse always shows the categories.
- The selected tab is the one for the area the current screen belongs to. A purchase's detail, whether reached from recording or from Logs, sits under Logs.
- The bar is fixed to the bottom of the screen and does not scroll with the content. The cart bar, when it shows, is fixed directly above it. The content scrolls above both bars and ends clear of them.
- The bar is not shown on the sign-in screens.
- No motion is specified.

## Accessibility

- The bar is a navigation landmark labeled "Main", as the shell sets out. Its tabs are read as a list.
- A screen reader announces which tab is selected.
- Each icon is decorative and carries empty alternative text, because the label already names the tab.
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
| The bar is a floating white card with rounded corners and a soft shadow, inset from the screen's edges | proposed | |
| Each tab shows an icon above its label. The selected tab has a filled icon and a bold dark label, and an unselected tab has an outline icon and a muted gray label. | proposed | |
| The bar is fixed to the bottom of the screen, and the cart bar is fixed directly above it | proposed | |
| The selected tab is set by one boolean prop per tab, because the template language cannot branch on an enum's value | proposed | |
| Icons are inline SVG drawn from simple shapes: a grid for Browse, a receipt for Logs and a person for Profile, each filled when selected and an outline otherwise | proposed | |

The bar's placement, its tabs and the rule that a tab does not remember where the employee was are recorded on [[information-architecture/employee-app]] and [[layout-patterns/employee-app-shell]].

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The designer asked for a 12 px inset, and Bootstrap's spacing scale has no step of that size. Does the definition keep the nearest step, spacing 3, or does the system add one? | Shivani Erlewad | The design system's spacing tokens are set |
| Do the inline SVG icons stay, or does an icon catalog replace them, and at what size? | Shivani Erlewad | The icon catalog exists |
| What does tapping the tab that is already selected do? | Shivani Erlewad | A screen of the bar has been designed |
| Do Browse, Logs and Profile read clearly as tab labels? | Shivani Erlewad | A click test on a prototype has been run |

## Related

- [[information-architecture/employee-app]] — the structure whose areas the bar links, and the decisions it records.
- [[layout-patterns/employee-app-shell]] — the shell that places the bar at the bottom of every screen.
