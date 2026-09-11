---
name: shopify-responsive-auditor
description: Audit and plan responsive adaptation for Shopify storefronts from a desktop-site URL, with optional theme-code inspection when Shopify CLI, theme files, or a Shopify connector are available. Use when ChatGPT needs to assess desktop-to-tablet/mobile behavior, discover responsive defects, define breakpoint and component rules, produce a configuration report, prioritize launch blockers, or generate safe file-level modification steps for an existing Shopify theme without redesigning the approved desktop experience.
---

# Shopify Responsive Auditor

## Objective

Turn one desktop storefront URL into a repeatable responsive-audit workflow. Discover the site's real page/component patterns, test them across screen widths, identify root causes, and return an implementation-ready configuration report plus modification plan. Preserve the approved desktop design unless the user explicitly asks to redesign it.

## Input contract

Accept a desktop storefront URL as the only required input.

Infer page coverage from the live site rather than asking the user to enumerate pages. Discover navigation, sitemap/routes, product/content templates, and shared components. Ask a follow-up question only when the storefront cannot be accessed, is password-protected, or the user has a critical business constraint that cannot be inferred.

If theme-code access is available through Shopify CLI, a connected Shopify tool, a repository, or uploaded theme files, use it for code-level diagnosis. If code access is unavailable, complete the visual/behavioral audit anyway and mark code-level causes as inferred rather than confirmed.

## Operating principles

1. Treat desktop as the visual source of truth unless desktop itself is broken.
2. Audit before modifying. Do not manufacture refactors for components that already behave correctly.
3. Separate global responsive rules from component-specific fixes.
4. Fix root causes, not symptoms. Do not hide layout bugs with global `overflow-x: hidden`.
5. Preserve Shopify Theme Editor configurability and current content/settings.
6. Prefer CSS/Grid/Flex and native HTML behavior over duplicated DOM or unnecessary JavaScript.
7. Protect shared components: verify every page/template that consumes a shared asset before changing it.
8. Preserve commerce, form, filtering, pagination, cart, and pricing logic unless a verified bug requires a logic change.
9. Classify issues by launch impact and only prioritize blockers and clear launch risks.
10. Re-test desktop after every mobile/tablet fix.

## Workflow

### Step 1: Discover the storefront

From the supplied URL:

- Inspect the main navigation and footer.
- Discover sitemap/routes when accessible.
- Group pages by archetype rather than by page name: homepage/landing, product detail, product directory/collection, pricing/configurator, editorial/listing, article/content, contact/form, FAQ/accordion, policy/long text, support/downloads, cart/commerce, and special campaign pages.
- Identify shared components such as header, footer, announcement bar, cards, carousels, video, subscribe, forms, product forms, cart drawer, breadcrumbs, filters, tabs, accordions, timelines, galleries, and reusable marketing sections.
- Choose representative pages for each archetype plus all high-conversion routes.

Do not hard-code a page inventory from previous projects.

### Step 2: Establish the responsive configuration

Read existing breakpoints first. Prefer the theme's current responsive system when coherent. If no coherent system exists, recommend this default baseline:

- Small mobile: <=479px
- Mobile: 480-749px
- Tablet: 750-1023px
- Desktop: >=1024px
- Large desktop: >=1440px

Do not add many near-duplicate breakpoints to solve isolated defects. Record existing legacy breakpoints separately and recommend consolidation only when it is safe and worthwhile.

Define and report:

- content/container widths
- page gutters
- section spacing scale
- typography scale
- card behavior
- media behavior
- touch-target minimums
- mobile navigation/footer behavior
- carousel rules
- image `sizes/srcset` expectations

Use `references/audit-checklist.md` for detailed checks.

### Step 3: Test representative widths

Default QA matrix:

- 1440
- 1024
- 768
- 430
- 390
- 375
- 360
- 320

If browser emulation is available, inspect the live layout at these widths. If only screenshots are possible, prioritize 1440, 768, 390, and 320 and clearly state the reduced coverage.

At each width, inspect actual element overflow and layout behavior; do not rely only on visual impression.

### Step 4: Diagnose at three levels

For every defect, distinguish:

**Visual symptom** — what the user sees.

**Layout/root cause** — e.g. fixed width, `min-width`, inline style overriding media query, inherited desktop alignment, duplicated clone content, wrong Grid/Flex rule, shared CSS missing from a page, fixed height, wrong object-fit, unhandled nested anchor, or breakpoint conflict.

**Implementation scope** — global token, shared component, template, section, snippet, asset, or JavaScript.

When code access exists, inspect the latest live/remote file before concluding. Do not diagnose from stale local code.

### Step 5: Apply pattern rules

Use `references/pattern-library.md` to select the correct mobile/tablet pattern. Key decisions include:

- compact peers -> multi-column grid when readable
- content-rich peers -> native horizontal swipe when stacking would make the page excessively long
- reading/form/policy content -> vertical flow, never carousel
- product directories -> choose single-column compact cards or a readable grid based on information density, not a fixed rule
- timelines -> convert complex desktop alternation into a single readable mobile flow
- nested mobile menus -> parent acts as disclosure; preserve a separate route to the parent page
- long mobile footers -> collapse menu groups with native disclosure behavior

Do not use `transform: scale()` to make desktop cards fit mobile.

### Step 6: Verify conversion and interaction

Audit the complete conversion path, not only static layout:

- navigation -> discovery -> offer/product -> CTA -> form/cart -> checkout entry
- filters and pagination
- add-to-cart/update/remove
- cart drawer
- forms, validation, success/error states
- accordions/tabs
- video playback/fallback
- mobile nested navigation

Do not submit real orders or irreversible forms unless explicitly authorized.

### Step 7: Classify issues

Use:

- **P0**: navigation, purchase, form, or page functionality broken; severe page breakage
- **P1**: obvious mobile/tablet defect, horizontal overflow, dead CTA, broken asset, unreadable content, major regression
- **P2**: minor visual inconsistency, code debt, naming, legacy breakpoint, environment-specific limitation, non-blocking optimization

Recommend fixing P0 and clear P1 before final launch QA. Record P2 without expanding scope.

### Step 8: Produce the configuration report and modification plan

Follow `references/report-template.md`.

The report must include:

- discovered page archetypes and shared components
- responsive configuration
- issue inventory with evidence, root cause, breakpoint, priority, and scope
- global rules vs local exceptions
- file/component-level modification sequence when code is available
- visual-only modification sequence when code is not available
- QA matrix and acceptance criteria
- deferred P2 items

Modification steps must be ordered so that foundations/shared components are fixed before dependent pages, then final whole-site regression QA.

## Code-level rules

When Shopify theme code is available:

- Inspect current remote/live files before editing.
- Prefer changing the smallest responsible file.
- Avoid touching `templates/*.json` or `config/settings_data.json` when CSS/Liquid can solve the issue.
- Preserve Theme Editor content/settings and user-configurable values.
- For inline Theme Editor styles that defeat responsive CSS, use component-scoped mobile ceilings/overrides rather than deleting editor controls.
- Use `min-width: 0` for Grid/Flex children that can overflow.
- Use `max-width: 100%` on responsive media where appropriate.
- Use `object-fit: contain` for product/cutout imagery and `cover` only for scene/banner imagery where cropping is intended.
- Do not use arbitrary fixed heights solely to equalize cards; use stretch/flex structure.
- Do not use JavaScript height measurement for ordinary card equalization.
- Do not duplicate desktop/mobile markup unless there is a documented accessibility or content-order reason.
- For duplicated carousel/gallery clones, ensure mobile/static modes do not expose duplicate content.
- When a card or item may be hidden dynamically, verify the remaining layout collapses gracefully.
- Preserve touch targets even when visual buttons/icons are compact: target ~48px, visual icon may be smaller.
- Keep responsive image `sizes` aligned with the actual rendered card width.

## Shared-component safety

Before changing any shared section/snippet/asset:

1. Find all consumers.
2. Test the change against each consumer.
3. Scope a page-specific exception only when the shared behavior should genuinely differ.
4. Avoid copy-pasting the shared component into page-specific variants just to fix CSS.

## Media and embedded video

Treat media failures as layered diagnostics:

1. Confirm the media element exists and has non-zero size.
2. Confirm the source URL/ID generated correctly.
3. Confirm desktop vs mobile/browser behavior.
4. Distinguish code failure from provider/browser/WebView restrictions.
5. Preserve a fallback link when an external embed is business-critical.

Do not repeatedly rewrite embed Liquid if the iframe renders correctly and the failure occurs only in a specific in-app browser. Record environment-specific incompatibility as P2 unless it blocks a major acquisition channel; in that case recommend a Shopify-hosted video fallback.

## Navigation and footer rules

For mobile nested navigation:

- Do not let a parent link with children immediately navigate before users can discover the submenu.
- Use the parent row as disclosure and provide an explicit parent/overview route inside the expanded submenu.
- Keep child links data-driven from Shopify Navigation; do not hard-code menu items.
- Keep touch rows >=48px and visible focus states.

For long mobile footers:

- Prefer native `details/summary` accordion groups.
- Default groups collapsed when appropriate.
- Make the full summary row clickable.
- Keep row heights and divider spacing consistent.
- Avoid extra top/bottom borders and accidental container padding that create blank bands.
- Preserve payment, legal, locale, social, and copyright content outside the accordion unless the design calls for otherwise.

## Typography rules

Do not shrink everything uniformly. Use role-based scaling and readability floors.

Typical starting ratios relative to approved desktop sizes:

- H1: laptop 0.82-0.88, mobile 0.60-0.68, small mobile 0.54-0.60
- H2: laptop 0.84-0.90, mobile 0.64-0.72, small mobile 0.58-0.65
- H3: laptop 0.88-0.94, mobile 0.72-0.80, small mobile 0.68-0.75
- Body: laptop 0.94-1.00, mobile 0.88-0.95, small mobile 0.85-0.92

Use component context to override these ratios. A dense editorial card may need a smaller semi-bold title while a hero must remain dominant.

## Card consistency

Within the same visual sibling group at a given breakpoint:

- equal width
- equal outer height when they are intended as peers
- consistent media region
- natural internal whitespace
- CTA/footer alignment when appropriate

Let the tallest content determine group height. Do not force unrelated cards across different sections to match.

## Final QA gate

After recommended fixes, run one final whole-site pass:

- responsive regression
- navigation
- conversion path
- cart/forms
- filters/pagination
- media/video
- shared components
- browser console
- broken assets/links
- obvious CLS/performance blockers
- theme validation/Theme Check when code access exists

If no P0/P1 remains, report `Launch Ready` and stop. Do not invent additional cleanup work.

## References

- Read `references/audit-checklist.md` for the complete responsive inspection checklist.
- Read `references/pattern-library.md` when choosing a mobile/tablet layout treatment for a component.
- Read `references/report-template.md` before producing the final configuration report and modification sequence.
