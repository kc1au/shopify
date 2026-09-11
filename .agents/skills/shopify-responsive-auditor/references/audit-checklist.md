# Responsive Audit Checklist

## 1. Global frame

- Viewport/meta tag correct.
- No page-level horizontal overflow at 320-430px.
- Container width uses available space rather than desktop fixed width.
- Full-bleed background is separated from constrained content width.
- Page gutters are consistent and not doubled by nested containers.
- Section padding scales down without collapsing hierarchy.
- Fixed/sticky elements do not cover content or CTA controls.
- Safe-area behavior is acceptable on mobile devices.

## 2. Breakpoints and cascade

- Inventory all media-query breakpoints.
- Flag near-duplicate breakpoints that create inconsistent states.
- Check later CSS files for overrides that cancel earlier responsive rules.
- Check inline `style` attributes from Theme Editor that outrank ordinary CSS.
- Check specificity escalation and unnecessary `!important` usage.
- Verify desktop rules are restored above mobile breakpoints.
- Verify a component loaded on one page also loads its required CSS on other pages.

## 3. Typography

- H1/H2/H3 hierarchy remains obvious.
- Long headings wrap naturally without orphaned fragments or overflow.
- Mobile card titles are not simply desktop titles squeezed into narrow cards.
- Dense cards can use semi-bold 600 rather than 700-900 when readability improves.
- Body text remains comfortably readable.
- Line height is not too tight after font-size reduction.
- Labels/badges remain legible.
- Inline editor-configured font sizes receive mobile ceilings when needed.

## 4. Grid and Flex

- Grid/Flex children that contain text/media have `min-width: 0` where necessary.
- `min-content` sizing does not create overflow.
- Gaps scale appropriately.
- Stacking order preserves the intended reading sequence.
- `order` rules do not create accessibility/content-order confusion.
- Hidden dynamic siblings do not leave empty tracks or carousel dead space.
- No `transform: scale()` is used to force a desktop layout into mobile.

## 5. Cards

- Peer cards are equal width.
- Peer cards are equal outer height only when visually intended.
- Media areas are consistent.
- Titles/excerpts use appropriate line clamp only when needed.
- CTA/footer aligns naturally toward the bottom if the design benefits.
- Avoid large empty zones caused by fixed/min heights.
- Card border radius/padding is not oversized on narrow screens.
- Whole-card links and nested action buttons do not conflict.

## 6. Mobile density decision

Use a 2-column grid when peer items are compact and remain readable at 320px.

Use native horizontal swipe when:
- there are 3+ content-rich siblings,
- stacked cards create excessive page length,
- each card needs near-full mobile width.

Horizontal swipe defaults:
- `overflow-x: auto`
- `scroll-snap-type: x mandatory`
- card width about 82-88vw
- 12-16px gap
- next-card peek
- no carousel JS, arrows, dots, or swipe hint for MVP unless needed

Never carousel:
- FAQ accordions
- forms
- policy/warranty text
- continuous reading content
- sequential setup instructions where all content must be visible in order

## 7. Images and media

- Product/cutout image -> `object-fit: contain`.
- Scene/banner/editorial image -> `cover` only when intentional crop is acceptable.
- `max-width: 100%` and correct responsive sizing.
- Image does not stretch vertically.
- Focal point survives crop at 320/390/768.
- `sizes` matches actual layout width after grid changes.
- Hidden duplicate/mobile media is not unnecessarily downloaded when avoidable.
- Infinite-loop gallery clones are not visible in static/mobile mode.
- SVG/logo aspect ratio is preserved.

## 8. Hero and first screen

- Main message fits without dominating the whole mobile viewport.
- CTA remains visible and tappable.
- Background image crop supports the message.
- Text does not overlay a busy/low-contrast region.
- Full-bleed behavior is correct on mobile.
- Header + hero interaction does not cause clipping or extra blank space.

## 9. Navigation

Desktop:
- hover/focus dropdown works
- parent route remains accessible
- submenu remains inside viewport

Mobile:
- hamburger opens/closes reliably
- parent with children expands before navigation
- explicit parent/overview link exists inside expanded menu
- child links are reachable
- disclosure chevron/state is clear
- rows >=48px touch height
- focus/keyboard states remain usable
- menu does not overflow screen height without scrolling

## 10. Footer

- Mobile footer is not dominated by long open link lists.
- Accordion rows have consistent height and separators.
- No unexplained blank band before first or after last menu group.
- Parent weight is not excessively bold.
- Plus/minus or chevron state is clear.
- Legal/payment/locale content remains accessible.
- Payment icons wrap cleanly at 320px.

## 11. Product directories / collections

- Decide information density before choosing grid count.
- Full ecommerce cards with image + long title + price + multiple CTAs usually need single-column mobile treatment.
- A compact multi-column grid is acceptable only if content remains readable at 320px.
- Prefer a compact mobile card variant rather than shrinking the desktop card wholesale.
- Product image should be the visual focus.
- Price and primary cart action can share a compact footer row.
- Icon-only cart actions need a large invisible touch area.
- Preserve product route access separately from add-to-cart.

## 12. Editorial/blog/listing

- Do not compress text-heavy vertical cards into unreadable 2-column cards.
- A useful mobile pattern is single-column outer list + horizontal card interior: metadata row, thumbnail, title/excerpt.
- Keep title weight/size proportional; semi-bold 600 is often better than heavy 700-900 in narrow card columns.
- Check line clamp does not hide nearly all meaning.
- Search/filter controls fit at 320px.
- Pagination adapts to mobile card count if client-side pagination is used.
- Recalculate pagination on breakpoint changes without duplicate listeners.

## 13. Timelines / process diagrams

- Desktop alternating left/right timelines often become awkward on mobile.
- Prefer one vertical rail on the left and one consistent content column on the right.
- Override inherited desktop text alignment on mobile.
- Use natural item height + modest bottom spacing.
- Keep nodes aligned with the first line/year/step label.
- Avoid a heavy rail or huge horizontal voids.

## 14. Forms

- Inputs/selects/textareas fit 320px.
- Labels remain associated and visible.
- Required/invalid states remain clear.
- Buttons >=48px touch height.
- Mobile keyboard/focus does not create horizontal overflow.
- Long consent/legal copy wraps naturally.
- Select arrows/icons do not collide with text.
- Success/error states do not shift layout badly.
- Shared form sections behave consistently across every page that uses them.

## 15. Accordions/tabs

- FAQ remains vertical and readable.
- Summary/tap row is large enough.
- Open state does not clip text.
- Tabs can wrap/scroll only when labels remain discoverable.
- Native `details/summary` is preferred for simple disclosure patterns.

## 16. Embedded video

- Wrapper has stable 16:9 ratio.
- iframe/video has non-zero width/height.
- Source/ID is correct.
- Desktop and mobile browsers tested separately.
- In-app WebView failure is distinguished from code failure.
- External-provider fallback link is visible when important.
- Consider Shopify-hosted video if an acquisition channel relies heavily on in-app browsers.

## 17. Commerce and conversion

- Product CTA route works.
- Add-to-cart works from every supported entry point.
- Cart drawer opens and is usable at 320px.
- Quantity/remove/update work.
- Subtotal renders correctly.
- Checkout entry works; do not complete payment during ordinary QA.
- Pricing/configurator/filter state survives responsive changes.
- No dead `#` CTA or obsolete route appears in the main funnel.

## 18. Performance quick check

Only flag meaningful launch issues:
- huge hero/mobile images
- duplicate media DOM/downloads
- autoplay/infinite effects causing obvious jank
- repeated resize listeners
- console errors
- severe layout shift
- third-party embed blocking interaction

Do not turn responsive QA into a full performance rewrite.

## 19. Final regression

- 1440 desktop source-of-truth preserved.
- 1024 intermediate state stable.
- 768 tablet not accidentally using phone-only treatment.
- 430/390 common phones correct.
- 360/320 stress test passes.
- Shared components pass on every consumer page.
