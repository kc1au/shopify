# Responsive Audit Report Template

Use this structure unless the user explicitly requests another format.

# Shopify Responsive Adaptation Report

## 1. Executive result

- Overall: PASS / NEED FIX / LAUNCH READY
- Highest priority: [short statement]
- Code access: Confirmed / Not available
- Coverage: [number of page archetypes, shared components, tested widths]

## 2. Discovered storefront architecture

Summarize page archetypes and shared components discovered from the URL. Do not dump every route unless useful.

## 3. Responsive configuration

| Item | Existing | Recommended/Accepted |
| --- | --- | --- |
| Small mobile | | <=479px |
| Mobile | | 480-749px |
| Tablet | | 750-1023px |
| Desktop | | >=1024px |
| Large desktop | | >=1440px |
| Mobile gutter | | |
| Section spacing | | |
| H1/H2/H3 scaling | | |
| Card policy | | |
| Touch target | | ~48px |
| Carousel policy | | |

If the existing theme already has a coherent breakpoint system, preserve it and record that system instead of forcing the defaults.

## 4. Findings

| Priority | Archetype/component | Width | Symptom | Root cause | Scope | Recommended action |
| --- | --- | ---: | --- | --- | --- | --- |
| P0/P1/P2 | | | | Confirmed/Inferred | Global/Shared/Local | |

For code-confirmed issues, name the responsible file(s). For visual-only audits, do not invent filenames.

## 5. Global foundation changes

List only rules that should apply across multiple templates/components. Examples:

- breakpoint normalization
- container/gutter correction
- shared heading ceiling
- shared image rule
- `min-width:0` overflow protection
- touch-target baseline

If no global changes are needed, explicitly say so.

## 6. Component modification sequence

Order work by dependency:

1. responsive foundation/tokens
2. shared header/footer/navigation
3. shared cards/media/components
4. page-archetype-specific exceptions
5. interaction/commerce fixes
6. final regression QA

For each step include:
- affected archetype/component
- exact problem
- target behavior by breakpoint
- files/selectors when confirmed
- what must remain unchanged
- acceptance criteria

## 7. QA matrix

| Width | Global frame | Navigation | Cards/media | Forms/cart | Result |
| ---: | --- | --- | --- | --- | --- |
| 1440 | | | | | |
| 1024 | | | | | |
| 768 | | | | | |
| 430 | | | | | |
| 390 | | | | | |
| 375 | | | | | |
| 360 | | | | | |
| 320 | | | | | |

## 8. Conversion-path QA

Report whether users can move through:

Discovery -> offer/product -> CTA -> form/cart -> checkout entry

Mention dead links, inaccessible submenu routes, broken filters/pagination, cart/form failures, or obsolete routes.

## 9. Deferred P2 items

Record non-blocking technical debt or environment-specific issues without expanding the current implementation scope.

## 10. Launch gate

Return one of:

- `NEED FIX - P0/P1 remain`
- `READY FOR FINAL QA - known P0/P1 resolved`
- `LAUNCH READY - final QA passed`

Do not add speculative cleanup after `LAUNCH READY`.

## Optional: Codex/implementation prompt

When the user asks for a modification prompt, generate one concise implementation prompt per logical step. Include:

- target behavior
- breakpoint scope
- exact confirmed files when known
- preserved behavior
- QA widths
- safe deployment constraints

For concurrent theme editing, include:

- read latest remote before editing
- do not full-theme push
- identify exact changed files
- push only modified files using `--only`
- use `--nodelete`
- avoid unchanged `templates/*.json` and `config/settings_data.json`
- merge remote changes first if the same file changed
