---
title: OTP
type: domain-object
template-version: 1
sources: []
related: []
created: 2026-11-17
updated: 2026-11-23
owner: domain
authorship: curated
confidence: medium
---

## Definition

An OTP, short for one-time password, is a code that works for a single sign-in. A person enters it after giving their mobile number, to show that they hold that phone. It is not a permanent password.

## Attributes

- code — text — the short code the person enters.

## Invariants

None.

## Lifecycle

An OTP is made for one sign-in. It works for a short time, and once it has been used, it cannot be used again.

## Related entities

- [[entities/profile]] — holds the mobile number the code is sent to.
