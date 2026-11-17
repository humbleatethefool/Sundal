---
title: Sundal app base
type: app-base
template-version: 1
sources: []
related: []
created: 2026-11-17
updated: 2026-11-17
owner: product
authorship: canonical
origination: originate
confidence: medium
---

## Summary

The Sundal app base is the foundation that every Sundal app stands on: the shared look and page frames that no single app owns. It is not an app, and it holds no features.


## Scope

A page attributes here when it serves Sundal as a whole and no one app's users would call it theirs. A page that serves only the employee app belongs to the employee app's module.


## What attributes here

- The design system: the colors, type, spacing and components every app shares.
- Layout patterns, such as the frame each app's pages sit in.
- Shared catalogs a design system names, such as the icon set.


## Boundaries

- App-wide rules, such as online only and English only, stay on [[modules/sundal]].
- Rules for the employee app, such as the offline behavior and the + and − buttons, stay on [[modules/sundal/employee-app]].


## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| Does the employee app's shell attribute here, or to the employee app's module? | Shivani Erlewad | The vendor app's shell is designed |
