---
title: Screen
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:modules/sundal/employee-app]]"
sources: []
related: ["[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The screen is the frame of an employee-app screen after sign-in. It paints the page color behind the content, and it leaves room at the bottom so the content ends clear of the fixed cart bar, action bar and tab bar. Every screen's content sits inside it.

Use it once on each screen after sign-in.
- Do put the page header, the content and the fixed bars inside it.
- Do not nest one inside another.
- Do not use it on the sign-in screens, which have no bars.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Frame | Required | A block as tall as the screen, in the page color. |
| Bottom room | Required | Space under the content, as tall as the stack of the fixed bars. |
| Content | Required | The screen's header, content and bars. |

## Variants

None. The frame has one configuration.

## Tokens & measurements

| Part | Value | Token or class |
|---|---|---|
| Fill | The page color | the project token `surface-page` |
| Side gutter | Spacing 3 on each side, the one left and right edge of every block on the screen, fixed bars included | `px-3` |
| Height | At least the screen's height | `min-vh-100` |
| Bottom room | Clears the cart bar or the action bar above the tab bar | the project token `size-bottom-room` |

## States

| State | Treatment |
|---|---|
| Default | The page color behind the content. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `children` | Content | None | Required | The screen's content, from the page header to the last block. |

The definition is `design/components/screen.json`, with its markup in `design/components/screen.html`.

## Behavior & interaction

- The frame does not scroll by itself. The screen scrolls, and the fixed bars stay put.
- The content ends clear of the fixed bars, so the last block is never hidden under one.
- No motion is specified.

## Accessibility

- The frame adds no landmark. The header, content and bars inside it carry their own.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The frame holds no text of its own.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Each screen sits on the page color, which is white, with its cards in the card color on top. The page color is its own token, so it can change without touching the cards | proposed | |
| The frame leaves room at the bottom for the fixed bars, so no screen sets its own padding | proposed | |
| The frame owns the side gutter, 16 px, and the blocks of a screen sit in one stack 16 px apart, so every block shares the same left and right edge and the same gap. Both come from the spacing scale, so the spacing token drives them. | proposed | |
| Text uses one system font. Every heading is bold, from the heading weight token. Every button label is semibold, from the button weight token. A price is bold, an item name semibold, and all muted text one color. The smallest text is 14 px, badges included, from the badge size token. | proposed | |
| Every rectangular corner on every screen takes the one default radius, the design system's `border-radius` token (16 px), so cards, boxes, photos, alerts and buttons agree and one change reaches them all. Pills and circles keep their own shape. | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|

## Related

- [[layout-patterns/employee-app-shell]] — the shell whose regions sit inside the screen.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose screens use the frame.
