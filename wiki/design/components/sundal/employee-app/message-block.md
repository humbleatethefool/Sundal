---
title: Message block
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/toast]]", "[[surfaces/sundal/employee-app/record-a-purchase]]", "[[product:modules/sundal/employee-app]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-18
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The message block fills a screen's content region with a message when the screen has nothing else to show. It stands in for an empty list, a failed load or no connection, says what happened and, where there is one, offers the next step. The employee app's screens use it.

Use it when a whole content region is replaced by a message.
- Do give it a title, and a body when the title alone does not say what to do.
- Do offer Retry on an error or offline message, so the employee can try again.
- Do not use it for the "You're offline" toast, which is a short message that leaves the screen as it is. That is the [[components/sundal/employee-app/toast]].
- Do not use it for a message about one line. That is the line notice.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The block, centered in the content region it replaces. |
| Title | Required | A short line saying what happened. |
| Body | Optional | One or two sentences giving the reason or the next step. |
| Action | Optional | A [[components/sundal/employee-app/button]], such as Retry or Browse snacks. |

## Variants

The block varies by the situation it states. The wording of each is supplied by the screen that uses it.

| Variant | Used when | Action |
|---|---|---|
| Empty | A list or cart has nothing in it | None, or a button that leads on, such as Browse snacks |
| Error | The server could not return or save what was asked | Retry |
| Offline | The phone has no connection when the employee taps something that needs the server | Retry |

## Tokens & measurements

None. No token set exists, so the gap is recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The title, the body and the action, centered in the region. |

Tapping the action replaces the block with the screen's own loading state.

## Props / API

None documented yet.

## Behavior & interaction

- The block fills the content region it replaces. The header and the tab bar stay in view.
- Tapping Retry repeats the step that failed, and nothing changes on the server for an offline message.
- The block holds no input and no other action.
- No motion is specified.

## Accessibility

- The message is announced as it appears.
- The action is reachable by keyboard and by a screen reader, and is named for what it does.
- Text meets a contrast ratio of 4.5 to 1.
- The action is at least 24 by 24 CSS pixels, and meets 3 to 1 against its background.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

Each message says what happened and then what to do, in the reader's words. It leaves out "please" and words that judge the reader, and it names no cause it does not know. Where the cause is unknown the title reads "Something went wrong" and the body says to try again. The wording follows the project's UX-writing standard. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| Empty, error and offline messages are one component, differing only in the wording and the action their screen supplies | proposed | |
| The block fills the content region and leaves the header and the tab bar in view | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| The project has no design system or token set. Which tokens do the block's color, type and spacing take? | Shivani Erlewad | The design system page exists |
| Does the block carry an icon or an illustration? | Shivani Erlewad | The design system page exists |

## Related

- [[components/sundal/employee-app/button]] — the control the block's action uses.
- [[components/sundal/employee-app/toast]] — the short message used instead when the screen should stay as it is.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose screens use the block, with their own wording.
- [[product:modules/sundal/employee-app]] — the module whose offline rules the offline variant follows.
