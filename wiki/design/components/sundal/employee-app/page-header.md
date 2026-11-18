---
title: Page header
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:modules/sundal/employee-app]]"
sources: []
related: ["[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/cart]]", "[[surfaces/sundal/employee-app/categories]]", "[[surfaces/sundal/employee-app/category-items]]", "[[surfaces/sundal/employee-app/purchase-detail]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The page header is the strip at the top of every employee-app screen after sign-in. It shows the screen's title, and on a screen below a tab it also holds the Back control. It tells the employee where they are.

Use it at the top of each screen after sign-in.
- Do show the screen's own title: the category's name on Category items, and "Cart" and "Purchase" on those screens.
- Do show Back on Category items and Purchase detail, and nowhere else.
- Do not show it on the sign-in screens.
- Do not put actions in it other than Back.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The strip, at the top of the screen. |
| Title | Required | The screen's title. |
| Back control | Optional | A control that returns to the screen above. |

## Variants

The header varies by whether it holds Back.

| Variant | Holds | Used on |
|---|---|---|
| Title only | The title | Categories, Cart, and the root screens of Logs and Profile |
| With Back | The Back control and the title | Category items and Purchase detail |

Content configurations: a long title, such as a long category name, is open under Open questions.

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The title, with Back where the variant has it. |
| Pressed | Feedback on Back while the employee's finger is on it. Its form waits for the design system. |
| Focus | A visible focus indication on Back. Its form waits for the design system. |

## Props / API

None documented yet.

## Behavior & interaction

- Tapping Back returns to the screen above. The destination of Back after recording a purchase is open under Open questions.
- The header stays in view at the top of the screen.
- No motion is specified.

## Accessibility

- The header is a banner landmark, as the shell sets out.
- The title is the screen's first heading, so a screen reader reads where the employee is first.
- Back is a button named "Back".
- Text meets a contrast ratio of 4.5 to 1, and Back meets 3 to 1 against its background.
- Back is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

A title is the screen's label from the information architecture, in sentence case, or the category's name on Category items. It takes no closing period. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
None. The header's placement and where Back shows are recorded on [[layout-patterns/employee-app-shell]].

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the header's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| How does a long category name show as the title: wrapped, or shortened with the full name reachable? | Shivani Erlewad | A screen of the header has been designed |
| Where does Back lead from Purchase detail after recording, when the cart is empty? | Shivani Erlewad | The Logs screen is designed |
| Does the Cart have a Back, given the tab bar is its only exit? | Shivani Erlewad | The shell's header is settled |

## Related

- [[layout-patterns/employee-app-shell]] — the shell that places the header at the top of every screen.
- [[surfaces/sundal/employee-app/cart]], [[surfaces/sundal/employee-app/categories]], [[surfaces/sundal/employee-app/category-items]] and [[surfaces/sundal/employee-app/purchase-detail]] — the surfaces whose titles and Back the header shows.
