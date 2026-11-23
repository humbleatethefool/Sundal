---
title: Sign in
type: feature
template-version: 1
sources: []
related: ["[[modules/sundal/employee-app]]", "[[prds/sundal]]"]
depends-on: []
created: 2026-11-19
updated: 2026-11-19
owner: product
authorship: canonical
origination: originate
confidence: medium
---


## Summary

Sign in lets an employee sign in to the employee app with their mobile number and a one-time code.


## Problem it solves

Each purchase belongs to one employee, so the app must know who is recording it. An employee ([[personas/employee]]) has one personal sign-in, active on one phone at a time, and records only their own purchases.


## User story or flow

As an employee, I want to sign in with my mobile number, so that my purchases are recorded as mine.


## Acceptance criteria

- **AC1.** A code works for one minute and for one sign-in only.
- **AC2.** Signing in on a second phone ends the sign-in on the first phone.
- **AC3.** The app keeps the employee signed in until they log out or sign in on another phone.
- **AC4.** After 5 wrong codes in a day, a mobile number gets no code and none is accepted until midnight Indian time.
- **AC5.** A mobile number with no profile gets no code.


## Quality attributes

None.


## Task flows

- [[flows/sundal/employee-app/sign-in]] — an employee signs in with their mobile number and a one-time code


## Surfaces

- **Mobile number** (form) — the employee enters their mobile number. States: loading, error.
- **OTP** (form) — the employee enters the six-digit code, or taps Resend once a minute has passed. States: loading, error.


## Success metrics & instrumentation

None.


## Boundaries

- Adding employees to Sundal is not part of this feature. The company admin adds them.


## Open questions

None.

