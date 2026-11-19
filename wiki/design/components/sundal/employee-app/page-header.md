---
title: Page header
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:modules/sundal/employee-app]]"
sources: []
related: ["[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The page header is the strip at the top of every employee-app screen after sign-in. It shows the screen's title in bold, and on a screen below a tab it also holds a round Back button at its start. It tells the employee where they are.

Use it at the top of each screen after sign-in.
- Do show the screen's own title: the category's name on Category items, and "Cart" and "Purchase" on those screens.
- Do show Back on Category items, and on Purchase detail only when the employee opened the purchase from Logs. Show it nowhere else.
- Do not show it on the sign-in screens.
- Do not put actions in it other than Back.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The strip, at the top of the screen. |
| Title | Required | The screen's title. |
| Back control | Optional | A round white button with an arrow and a soft shadow, which returns to the screen above. |

## Variants

The header varies by whether it holds Back.

| Variant | Holds | Used on |
|---|---|---|
| Title only | The title | Categories, Cart, the root screens of Logs and Profile, and Purchase detail after recording |
| With Back | The Back control and the title | Category items, and Purchase detail when opened from Logs |

Content configurations: a long title, such as a long category name, is open under Open questions.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Strip | Stays at the top of the screen, in the page color | `sticky-top`, the project token `surface-page` |
| Title | Bold, large, wrapping when it is long | `h4`, `fw-bold`, `text-break` |
| Back button | 44 px circle in the card color with a soft shadow, holding an arrow | `rounded-circle`, `shadow-sm`, the project tokens `surface-card` and `size-round-button` |
| Spacing | Spacing 3 between the parts and above the strip. It adds no side space: the screen frame owns the side gutter, so the title lines up with the content. | `gap-3`, `pt-3` |
| Minimum strip width | 20 rem, so a header keeps its shape when its container sets no width | an inline `min-width` |

## States

| State | Treatment |
|---|---|
| Default | The title, with Back where the variant has it. |
| Pressed | Feedback on Back while the employee's finger is on it. Its form waits for the design system. |
| Focus | A visible focus indication on Back. Its form waits for the design system. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `title` | Text | None | Required | The screen's title. |
| `back` | Boolean | `false` | Optional | Shows the round Back button. |
| `children` | Button | None | Required when `back` is on | The Back button: a button of the link variant labeled "Back", stretched invisibly over the round shape. |

The Back button is a prop because a prototype links only a button. The definition is `design/components/page-header.json`, with its markup in `design/components/page-header.html`.

## Behavior & interaction

- Tapping Back returns to the screen the employee came from. Purchase detail has no Back after recording, so the employee leaves it by the tab bar.
- The header stays in view at the top of the screen.
- No motion is specified.

## Accessibility

- The header is a banner landmark, as the shell sets out.
- The title is the screen's first heading, so a screen reader reads where the employee is first.
- Back is a button named "Back". The arrow in the round shape is decorative, and the button is stretched invisibly over the shape.
- The invisible button shows no focus ring of its own. A visible focus indication waits for the design system.
- Text meets a contrast ratio of 4.5 to 1, and Back meets 3 to 1 against its background.
- Back is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

A title is the screen's label from the information architecture, in sentence case, or the category's name on Category items. It takes no closing period. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Back is a round white button with an arrow, after the headers of Blinkit, Zepto and Instamart, and it has no label | proposed | |
| The title is bold and large, at the start of the strip beside Back, and the strip stays at the top of the screen | proposed | |

Where the header sits and where Back shows are recorded on [[layout-patterns/employee-app-shell]].

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| How does a long category name show as the title: wrapped, or shortened with the full name reachable? | Shivani Erlewad | A screen of the header has been designed |
| Does the Cart have a Back, given the tab bar is its only exit? | Shivani Erlewad | The shell's header is settled |
| How does the round Back button show keyboard focus, when its invisible button shows none? | Shivani Erlewad | The design system page exists |

## Related

- [[layout-patterns/employee-app-shell]] — the shell that places the header at the top of every screen.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose screens show their title in the header, with Back on Category items, and on Purchase detail when opened from Logs.
