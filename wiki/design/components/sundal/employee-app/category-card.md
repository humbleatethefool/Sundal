---
title: Category card
type: ui-component
template-version: 2
status: draft
realizes:
  - "[[product:features/sundal/employee-app/record-a-purchase]]"
sources: []
related: ["[[surfaces/sundal/employee-app/record-a-purchase]]"]
invalidates: []
created: 2026-11-18
updated: 2026-11-19
owner: design
authorship: curated
origination: originate
confidence: low
---

## Purpose & usage

The category card shows one of the vendor's categories as a card: a colored rounded box, different for each category, with the category's name as a link below it. It is the card the Categories screen lays out in a grid. Tapping the link opens that category's items.

Use it for a category in the grid of categories.
- Do keep it to the box and the name link.
- Do not use it for an item. An item has a description, a price and an action, and has its own card.
- Do not add another control. The name link is the only one.

## Anatomy

| Part | Required | What it is |
|---|---|---|
| Container | Required | The whole card: the box and the link under it. |
| Box | Required | A rounded square in a pale color that differs for each category. It holds the category's image when it has one, and is plain otherwise. It is not tappable. |
| Name link | Required | The category's name as a link under the box, centered, which opens the category's items. |

## Variants

None. The card has one configuration. Its content varies: each category takes its own box color, a category whose image is missing or fails to load shows the plain colored box, and a long name wraps onto more lines.

## Tokens & measurements

The definition uses Bootstrap's classes only, so the design system's tokens restyle it once they exist.

| Part | Value | Token or class |
|---|---|---|
| Box fill | A tone from the category palette, yellow when none is set | the project tokens `category-yellow`, `category-blue`, `category-coral`, `category-lavender`, `category-peach` and `category-teal` |
| Box shape | Square, rounded | `ratio-1x1`, `rounded` |
| Image, when shown | Fitted inside the box with padding | `object-fit-contain`, `p-3` |
| Gap between box and link | Spacing 1 | `mb-1` |
| Name link | A link-style button, stretched to the card's width so a long name wraps | `btn-link`, `d-grid` |
| Minimum card width | 7 rem, so a card stays a square box when its container does not set a width | an inline `min-width` |
| Name width | Follows the card, never the name, so a long name wraps and does not widen the card | an inline `width` of 0 with a `min-width` of 100% |

The box colors, the image padding and the name's line limit have no fitting token, so they are recorded under Open questions.

## States

| State | Treatment |
|---|---|
| Default | The colored box, with the name link below. |
| Pressed | Feedback on the name link while the employee's finger is on it. Its form waits for the design system. |
| Focus | A visible focus indication on the name link. Its form waits for the design system. |
| Placeholder | A card-shaped placeholder shows while the categories load. |

## Props / API

| Prop | Type | Default | Required | What it does |
|---|---|---|---|---|
| `tone` | One of yellow, blue, coral, lavender, peach, teal | Yellow | Optional | The box's color, a tone from the category palette. Each category takes a different one. |
| `image` | Image address | None | Optional | The category's picture, shown inside the box. Left out, the box is plain. |
| `children` | Button | None | Required | The link under the box: a button of the link variant whose label is the category's name. It opens the category's items. |

The link is a prop because a prototype links only a button. The definition is `design/components/category-card.json`, with its markup in `design/components/category-card.html`.

## Behavior & interaction

- Tapping the name link opens that category's items. The box is not tappable.
- The card takes its width from the grid it sits in, and cards in one grid share one size and one image shape.
- A long name wraps onto more lines.
- No motion is specified.

## Accessibility

- The control is the name link, named by its own text. The box is decorative, and its image carries empty alternative text, because the name already says what it shows.
- The link shows the browser's own focus indication until the design system sets one.
- Text meets a contrast ratio of 4.5 to 1, and the card's edge meets 3 to 1 against the screen behind it.
- The card is at least 24 by 24 CSS pixels. Its size for a thumb is settled with the design system.

## Platform variations

None. The component is shown on phones only.

## Content guidelines

The name is the vendor's own text and shows in full, wrapping where it must. English only, so no translation or right-to-left layout applies.

## Decisions

| Decision | State | Decided |
|---|---|---|
| The card shows no item count | proposed | |
| Each category shows a pale colored rounded box, a different color for each, with its name as a link below it | proposed | |
| The box colors come from a palette of six project tokens, so each category's color is a brand choice and none repeats the primary green | proposed | |
| The name link is the only control: the box is not tappable | proposed | |

## Open questions

| Question | Owner | Resume condition |
|---|---|---|
| What shape and size is the category image, if the box shows one, and how many lines may a name wrap onto? | Shivani Erlewad | The design system page exists |
| Is a category image required when the vendor creates a category? | Shivani Erlewad | The vendor's catalog screens are designed |
| The name link is a smaller tap target than the whole card was. Should the box open the category too? | Shivani Erlewad | A click test on a prototype has been run |
| Which tone does a category take: the next unused one in order, or one the vendor picks? | Shivani Erlewad | The vendor's catalog screens are designed |

## Related

- [[surfaces/sundal/employee-app/record-a-purchase]] — the surface whose Categories screen lays the cards out.
