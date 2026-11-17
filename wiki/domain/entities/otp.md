---
title: OTP
type: domain-object
template-version: 1
sources: []
related: []
created: 2026-11-17
updated: 2026-11-17
owner: domain
authorship: curated
confidence: medium
---

## Definition

An OTP, short for one-time password, is a code that works for a single sign-in. The employee enters it after their mobile number to sign in. It is not a permanent password.

## Attributes

- code — number — the six-digit one-time code the employee enters.

## Invariants

None.

## Lifecycle

An OTP is made for one sign-in. It works for one minute, and once it has been used, it cannot be used again.

## Related entities

- [[entities/profile]] — holds the mobile number the employee signs in with.
