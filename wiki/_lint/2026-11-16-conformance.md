---
type: conformance-report
created: 2026-11-16
scope: tree
---

# Wiki Conformance Audit — 2026-11-16

**Verdict: PASS** — 0 errors, 0 warnings; 1 pages audited (tree), 0 not audited; 0 legacy, 0 pre-versioning, 0 unstamped pages.

## Findings

None.

## Legacy pages

None.

## Pre-versioning pages

None.

## Unstamped pages

None.

## Sections outside the template

None.

## Not audited

None.

## Check outcomes

| Check | Family | Severity | Outcome | Findings |
|---|---|---|---|---|
| `template-sections` | template | error | ran | 0 |
| `template-extra-sections` | template | info | ran | 0 |
| `template-bullets` | template | error | not applicable | — |
| `template-owner` | template | error | ran | 0 |
| `template-frontmatter` | template | error | ran | 0 |
| `template-version-valid` | template | error | ran | 0 |
| `empty-section` | completeness | error | ran | 0 |
| `pending-slot` | completeness | error | ran | 0 |
| `table-columns` | completeness | error | ran | 0 |
| `unsubstituted-token` | completeness | error | ran | 0 |
| `template-example-line` | completeness | error | ran | 0 |
| `unsubstituted-placeholder` | completeness | error | ran | 0 |
| `callout-type` | content | error | ran | 0 |
| `callout-status-restatement` | content | warning | ran | 0 |
| `row-ids` | content | error | not applicable | — |
| `template-excluded-sections` | template | error | not applicable | — |
| `template-lives-at` | template | error | ran | 0 |
| `template-module-page` | template | error | not applicable | — |
| `inbound-regression` | graph | warning | not applicable | — |
| `variant-sections` | template | error | not applicable | — |
| `required-section-content` | completeness | error | not applicable | — |
| `section-order` | template | error | ran | 0 |
| `heading-restatement` | content | error | ran | 0 |
| `code-pointer` | content | error | ran | 0 |
| `fold-citation` | content | error | not applicable | — |
| `cell-grammar` | cells | error | not applicable | — |
| `flow-step-coverage` | cells | warning | not applicable | — |
| `surface-action-kinds` | cells | error | not applicable | — |
| `bullet-qualifier` | cells | error | not applicable | — |
| `type-reference-agreement` | cells | error | not applicable | — |
| `common-fields-target` | cells | error | not applicable | — |
| `common-field-clash` | cells | error | not applicable | — |
| `surface-kind` | cells | error | not applicable | — |
| `surface-placement` | cells | error | not applicable | — |
| `surface-unreached` | cells | warning | not applicable | — |
| `surface-same-as` | cells | error | not applicable | — |
| `sitemap-structure` | cells | error | not applicable | — |
| `sitemap-composition` | cells | error | not applicable | — |
| `journey-structure` | cells | error | not applicable | — |
| `journey-title` | content | error | not applicable | — |
| `catalog-code-column` | cells | error | not applicable | — |
| `layout-pattern-structure` | cells | error | not applicable | — |
| `layout-pattern-coverage` | cells | warning | not applicable | — |
| `layout-pattern-fit` | cells | warning | not applicable | — |
| `sitemap-node-coverage` | cells | warning | not applicable | — |
| `journey-stage-coverage` | cells | warning | not applicable | — |
| `journey-stage-flow-mismatch` | cells | warning | not applicable | — |
| `journey-role-mismatch` | cells | warning | not applicable | — |
| `journey-uncited` | cells | warning | not applicable | — |
| `journey-walk-gap` | cells | warning | not applicable | — |
| `journey-stage-no-flow` | cells | warning | not applicable | — |

## Not checked by this audit

- A variant-form page carries the section set of the variant it picked — `wiki-template-labels` §Template labels
- A deviation-form page follows the deviation its template states — `wiki-template-labels` §Template labels
- A product page uses no implementation vocabulary — `wiki-page-content-rules` §Product sub-wiki authoring
- A page whose subject is not an external or code artifact names no code symbol — a class, function, method, or variable that exists only in code; names in an external contract stay, except on product pages — `wiki-page-content-rules` §Code citations
- A page follows the presentation defaults — `wiki-authoring-spec` §Presentation defaults
- Each section follows its template comment's instruction — including the cardinality, ownership and provenance minimums several templates state there as MUST or REQUIRES: at least two options under a `daci-record`'s `## Options considered`, a named individual as its Approver, a minimum of five Q&A pairs with one trade-off question on a `pr-faq`, an owner and a date on every action item, a cited source behind every `competitor-profile` claim, a quantified result on a `case-study`, at least one write-failure E path on a mutating `task-flow`, and an assessor independent of the control owner on a `compliance-record`. No check family reads a comment-stated constraint: the comment is prose an author reads, and matching it would mean resolving what the section's content means — the page's template (section comments)
- A callout sits inside a section and does not replace one — `wiki-page-content-rules` §Callouts
- A page follows the cross-cutting policies its project records on its own policy pages — `wiki-entity-data-model` §Data model
- A body-level closed vocabulary is used as its template defines it — a `test-scenario` Priority cell in P0/P1/P2, a surface `kind` transcribed from its feature's `## Surfaces` inventory rather than invented, a `risk-register` response strategy among the five it names, a `compliance-record` result among the four its assessment vocabulary names. The audit checks a cell's value where the template's `Cells:` label declares its grammar; a vocabulary stated only in prose stays judgment, because matching it means resolving which cell of which table a value sits in, and stays in the template's body comment where the author reads it — `wiki-template-labels` §Template labels
- A `ui-surface` action's `Leads to` names the destination the action really reaches, and each `when` condition holds as written. `surface-link` checks the destination's form and that its target is a named surface or a component, not that it is the right one — `wiki-surface-cell-grammars` §Surface cell grammars
- A surface's `Opened from` names a pattern region that really opens it, on every page of each application whose pages cite the pattern; a pattern nested inside some pages only, such as a detail layout, places the surface in the whole application. `pattern-region-refs` checks that the pattern exists and that its Regions table holds the Id, not that the region opens the surface — `wiki-surface-placement-cell-grammars` §Surface placement cell grammars
- A step a surface lists under `Flow steps` really happens on that surface. `flow-steps` checks that the flow lists the step and the page lists the flow, not where the step takes place — `wiki-surface-cell-grammars` §Surface cell grammars
- A Field inventory `Source` names the field the row's label shows. `field-source` checks that the field exists on the entity it links, not what the field means — `wiki-entity-cell-grammars` §Entity cell grammars
- An entity's `Example` is invented rather than copied from a real record, personal names and street addresses included. `typed-example` checks the value's form, and masks only the `Email`, `Phone` and `Secret` types it can recognize — `wiki-entity-cell-grammars` §Entity cell grammars
- A landmark role a layout pattern gives more than one region is labeled, and the Landmark cell's note says how. `landmark` checks that the cell opens with a role, not its note — `wiki-layout-pattern-cell-grammars` §Layout-pattern cell grammars
- A component variant an action's `Consequence` names exists on that `ui-component` page. `Leads to` names the component, and the variant stays in prose, because a component's variants are table rows rather than headings a link can name — `wiki-surface-cell-grammars` §Surface cell grammars
- A `test-scenario` row's flow-step reference names a step its flow declares. The neighboring `Verifies` cell is checked and this one is not, because the step reference is a parenthetical inside a free-text cell with no fixed grammar — the anchor `Verifies` has and this does not — `wiki-page-ids` §Row and criterion ids
- A `catalog`'s `## Entries` table uses the columns its own set needs. No column is fixed: the template licenses adapting them, and of the catalogs deployed across the instances most rename the identity and definition columns to fit the set, so a `Columns:` declaration here would report conforming pages — `wiki-template-labels` §Template labels
- A `mirror` or `link-only` page's pointer resolves, and a page whose canonical copy lives outside the wiki declares the mode. `/wiki-lint` reads the presence of an `http` URL on a page that declares one of the two modes; it fetches nothing, and a sub-wiki's origination default is authoring guidance no engine applies — `wiki-federation-model` §Origination modes
