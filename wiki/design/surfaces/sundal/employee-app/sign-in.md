---
title: Sign in
type: ui-surface
template-version: 2
feature: "[[product:features/sundal/employee-app/sign-in]]"
flows:
  - "[[product:flows/sundal/employee-app/sign-in]]"
platforms: [mobile]
sources: []
related: ["[[components/sundal/employee-app/button]]", "[[components/sundal/employee-app/screen]]", "[[components/sundal/employee-app/toast]]", "[[information-architecture/employee-app]]", "[[journeys/employee-record-a-purchase]]", "[[layout-patterns/employee-app-shell]]", "[[surfaces/sundal/employee-app/record-a-purchase]]", "[[domain:entities/otp]]", "[[domain:entities/profile]]", "[[product:features/sundal/employee-app/sign-in]]", "[[product:flows/sundal/employee-app/sign-in]]", "[[product:modules/sundal/employee-app]]", "[[product:personas/employee]]"]
invalidates: []
created: 2026-11-19
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Surface reference

The employee enters their mobile number and then the one-time code they receive, to sign in.

## Platform scope

Mobile only, in one layout for the compact width class, with no per-platform deltas.

## Surfaces

### Mobile number (form)

The employee enters the mobile number their company admin added and asks for a code.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] mobile-number
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] sign-in
- **Flow steps** — [[product:flows/sundal/employee-app/sign-in]] S1, S2, A1, A2, E1, E5, E6, T1, T2, T3
- **Layout patterns** — None.
- **Layout intent** — A page, because it is the first screen of a signed-out employee and holds one short task. The employee app shell sets the page color and the side gutter through the [[design:components/sundal/employee-app/screen]], and this screen shows none of the shell's header, cart bar or tab bar, because the employee has not signed in. The content runs top to bottom in one column: a heading, one line of helper text, the mobile number field with a fixed "+91" before it, and the Continue button. The eye meets the heading first and the field second. Continue is a full-width [[design:components/sundal/employee-app/button]] under the field, so the thumb reaches it. The content sits in the upper part of the screen so the on-screen keyboard does not cover the button.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Sign in | static | text, as the heading | Always |
  | Helper line | static | text, "We'll send a 6-digit code to this number." | Always |
  | Mobile number | [[domain:entities/profile]] `mobile number` | ten digits, with "+91" shown before the field | Always |
  | Field message | system: the number is not registered, or the limit has been reached | text under the field | Only after Continue returns E1 or E6 |

- **Input rules** —

  | Field | Control | Required | Validation | Help | Default |
  |---|---|---|---|---|---|
  | Mobile number | free text that takes digits only, with a numeric keyboard | Required | Exactly ten digits. The field takes digits only and stops at ten, and Continue stays turned off until all ten are in, so it needs no message and no check. | Helper text: the helper line under the heading, which stays visible | None. |
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Continue, a [[design:components/sundal/employee-app/button]] | primary | Ten digits are entered, and the phone is online | Asks the server to send a code, blocks a second tap while it does, and shows the sending state | [[design:surfaces/sundal/employee-app/sign-in#otp-form]] |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The send failed, or the phone is offline | Repeats the last tap and shows the sending state | — |

- **Resilience states** —
  - **Loading** — The inline element loads: Continue shows its sending state, reading "Sending code", and cannot be tapped. The field keeps the number and stays as it is.
  - **Empty** — None. The screen is a form and shows no list.
  - **Error** — Four errors occur. When the number belongs to no profile (E1), the message under the field reads "This number is not registered. Check it and try again." and the entered number stays. When the number has had 5 wrong codes today (E6), the message under the field reads "No more codes can be tried today. Try again tomorrow." When the server cannot send the code (E4), a message above Continue reads "Something went wrong. Try again." with Retry, and the number stays. When the phone is offline (E5), a message above Continue reads "You're offline" with Retry, and the number stays. When the phone goes offline while the form is on screen, the [[design:components/sundal/employee-app/toast]] says "You're offline" and nothing else changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — None. The form has one field, so it has no half-completed state beyond the turned-off Continue.
  - **Access-gated** — None. Only a signed-out employee sees this screen. An employee the app keeps signed in opens on the Categories list instead (A1).
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Ideal, Continue turned off | Ideal, Continue on | The employee enters the tenth digit | Continue turns on |
  | Ideal | Loading | The employee taps Continue | Continue shows "Sending code" and the field stays |
  | Loading | OTP screen | The server sends the code | The OTP screen replaces this one |
  | Loading | Error | The server finds no profile, has reached the limit, cannot send, or the phone is offline | The matching message shows, and the number stays |
  | Error | Loading | The employee taps Retry or Continue again | The message gives way to the sending state |

- **Accessibility** — The heading is the first heading, and the field is the first thing to take focus, with the numeric keyboard open. The focus order is the field, then Continue. Each field has a visible label and states its format before the employee types. An error message under the field is announced as it appears and is linked to the field. Continue says when it is turned off through its state, not through color alone. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

### OTP (form)

The employee enters the six-digit code that was sent to their number.

- **Platforms** — mobile
- **Container** — page
- **Node** — [[design:information-architecture/employee-app]] otp
- **Shown in** — None.
- **Opened from** — None.
- **Journey stages** — [[design:journeys/employee-record-a-purchase]] sign-in
- **Flow steps** — [[product:flows/sundal/employee-app/sign-in]] S3, S4, S5, S6, A3, A4, E2, E3, E4, E5, E6, T1, T3
- **Layout patterns** — None.
- **Layout intent** — A page, because it is the second step of the same short task. It follows the Mobile number screen's arrangement, with no header, cart bar or tab bar. The content runs top to bottom in one column: a heading, a line saying where the code went with a Change number link beside it, the code field, the Sign in button and, below it, the Resend control. The eye meets the heading first and the code field second. The code field is one row of six digits that fills the width. Sign in is the full-width primary [[design:components/sundal/employee-app/button]]. Resend sits below it as a quieter text control, so it is not mistaken for the main action.
- **Field inventory** —

  | Label | Source | Format | Condition (when shown) |
  |---|---|---|---|
  | Enter the code | static | text, as the heading | Always |
  | Sent to | system: the mobile number entered on the Mobile number screen | text, such as "Code sent to +91 98765 43210" | Always |
  | Code | [[domain:entities/otp]] `code` | six digits | Always |
  | Resend timer | system: seconds since the code was sent | text, such as "Resend code in 0:42" | Until one minute has passed since the code was sent |
  | Field message | system: the code was not accepted, has expired, or the limit has been reached | text under the field | Only after E2, E3 or E6 |

- **Input rules** —

  | Field | Control | Required | Validation | Help | Default |
  |---|---|---|---|---|---|
  | Code | free text that takes digits only, with a numeric keyboard | Required | Exactly six digits. The field takes digits only and stops at six, and Sign in stays turned off until all six are in, so it needs no message and no check. | Helper text: the "Sent to" line, which stays visible | None. |
- **Actions** —

  | Label | Kind | Precondition | Consequence | Leads to |
  |---|---|---|---|---|
  | Sign in, a [[design:components/sundal/employee-app/button]] | primary | Six digits are entered, and the phone is online | Asks the server to check the code, blocks a second tap while it does, and shows the checking state | [[design:surfaces/sundal/employee-app/record-a-purchase#categories-list]] |
  | Change number | nav | Always | Opens the Mobile number screen with the number still filled in. The code already sent is left to expire. | [[design:surfaces/sundal/employee-app/sign-in#mobile-number-form]] |
  | Resend code | secondary | One minute has passed since the code was sent, and the phone is online | Sends a new code, shows the timer again from one minute and clears the code field | — |
  | Retry, a [[design:components/sundal/employee-app/button]] | secondary | The check or the resend failed, or the phone is offline | Repeats the last tap | — |

- **Resilience states** —
  - **Loading** — The inline element loads: Sign in shows its checking state, reading "Checking code", and cannot be tapped. The digits stay in the field.
  - **Empty** — None. The screen is a form and shows no list.
  - **Error** — Five errors occur. When the code is wrong or was already used (E2), the message under the field reads "The code was not accepted. Check it and try again." and the field keeps the digits so the employee can change one. When the code has expired (E3), the message reads "The code has expired. Tap Resend code to get a new one." and Resend code is on. When the number has had 5 wrong codes today (E6), the message reads "No more codes can be tried today. Try again tomorrow." and Sign in and Resend code stay turned off. When the server cannot check the code or send a new one (E4), a message above Sign in reads "Something went wrong. Try again." with Retry. When the phone is offline (E5), a message above Sign in reads "You're offline" with Retry. When the phone goes offline while the form is on screen, the [[design:components/sundal/employee-app/toast]] says "You're offline" and nothing else changes. The offline rules are the employee app's, in [[product:modules/sundal/employee-app]].
  - **Partial** — None. The form has one field, so it has no half-completed state beyond the turned-off Sign in.
  - **Access-gated** — None. Only a signed-out employee who has asked for a code reaches this screen.
- **State transitions** —

  | From | To | Trigger | What changes |
  |---|---|---|---|
  | Ideal, Sign in turned off | Ideal, Sign in on | The employee enters the sixth digit | Sign in turns on |
  | Ideal | Loading | The employee taps Sign in | Sign in shows "Checking code" and the digits stay |
  | Loading | Categories | The server accepts the code | The Categories list replaces this screen, with Browse selected |
  | Loading | Error | The code is not accepted or has expired, the limit is reached, the server fails, or the phone is offline | The matching message shows |
  | Ideal | Ideal | One minute passes since the code was sent | The timer gives way to Resend code, which turns on |
  | Ideal | Ideal | The employee taps Resend code | A new code is sent, the field clears and the timer starts again |

- **Accessibility** — The heading is the first heading, and the code field is the first thing to take focus, with the numeric keyboard open. The focus order is the Change number link, the field, Sign in, then Resend code. The field has a visible label and states its length before the employee types. The timer is announced when Resend code turns on, not each second. An error message is announced as it appears and is linked to the field. Text meets the 4.5 to 1 contrast ratio of WCAG 2.2 level AA.
- **Platform variations** — None. The screen is shown in one layout, since the app is phones only.

## Platform variations

None. The surfaces are shown in the one compact layout.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The mobile number is ten digits with a fixed "+91" shown before the field, since the app is built for India only | proposed | |
| Continue and Sign in stay turned off until the field is full, so the forms need no format validation message | proposed | |
| The sign-in screens show a heading in the content region and no page header, because the page header is not used on them | proposed | |
| The employee's entry is kept after every error, so nothing has to be typed again | proposed | |
| Resend code shows a one-minute countdown beside it while it is not available, and turns on when the code expires | proposed | |
| The message for a number that is not registered names the number's state and the next step: "This number is not registered. Check it and try again." | proposed | |
| Resend code and the countdown sit below the primary button, as a quieter control | proposed | |
| The OTP screen offers a Change number link beside the line that says where the code went, so a mistyped number is corrected without a Back control | proposed | |
| The sign-in screens follow no layout pattern: the employee app shell lists no form surface and its header, cart bar and tab bar do not show before sign-in | proposed | |
| An offline or failed request shows its message above the button, not in place of the form, so the entry stays in view | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| No component page covers a text field, the code field or the Resend control. Which components carry them? | Shivani Erlewad | The component specs for the fields are written |
| The module's offline rule says the screen shows "You're offline" with Retry. On a form this would hide the employee's entry. Does the rule allow the message above the button? | Shivani Erlewad | The offline rule is next reviewed |
| Should the mobile number show in full on the OTP screen, or masked? | Shivani Erlewad | A click test on a prototype has been run |
| Does the OTP field accept a code filled in by the phone's message app? | Shivani Erlewad | A click test on a prototype has been run |

## Related

- [[components/sundal/employee-app/button]] — the control for Continue, Sign in and Retry.
- [[components/sundal/employee-app/screen]] — the frame that sets the page color and the side gutter.
- [[components/sundal/employee-app/toast]] — the message that says the phone is offline.
- [[information-architecture/employee-app]] — the sitemap nodes these screens sit on.
- [[journeys/employee-record-a-purchase]] — the journey whose sign-in stage these screens serve.
- [[layout-patterns/employee-app-shell]] — the shell whose bars these screens leave out.
- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface page for the Categories list the employee lands on.
- [[domain:entities/otp]] — the entity the code field matches.
- [[domain:entities/profile]] — the entity whose mobile number the first field matches.
- [[product:features/sundal/employee-app/sign-in]] — the feature these screens realize.
- [[product:flows/sundal/employee-app/sign-in]] — the flow whose steps happen on these screens.
- [[product:modules/sundal/employee-app]] — the employee app's module page, which holds its offline behavior.
- [[product:personas/employee]] — the person using the screens.
