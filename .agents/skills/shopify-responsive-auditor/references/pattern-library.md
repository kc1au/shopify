# Responsive Pattern Library

## Decision table

| Component situation | Preferred mobile treatment | Avoid |
| --- | --- | --- |
| 2-4 compact peer cards | 2-column grid if readable at 320px | Shrinking desktop cards with transforms |
| 3+ content-rich cards | Native horizontal scroll + snap | Very long stacked page; JS carousel by default |
| Product listing with rich ecommerce controls | Single-column compact product card | 3-column full desktop purchase cards |
| Blog/article listing | Single-column list; horizontal card interior | Narrow 2-column text-heavy cards |
| FAQ / policy / long copy | Natural vertical flow | Carousel |
| Desktop alternating timeline | Left rail + single content column | Preserving alternating left/right alignment |
| Nested mobile navigation | Parent disclosure + overview link | Parent immediately navigating away |
| Long footer menus | Collapsed `details/summary` groups | All child links open by default |
| External video | Responsive 16:9 + fallback | Fixed pixel height; endless embed rewrites without browser diagnosis |
| Product image | Contain in stable media region | Cover/cropping unless intentional |
| Scene/banner image | Cover with focal-point QA | Contain with unwanted letterboxing |

## Pattern: native horizontal peers

Use when content-rich sibling cards would make mobile pages excessively long.

Behavior:
- single horizontal track
- card width 82-88vw
- 12-16px gap
- `overflow-x:auto`
- `scroll-snap-type:x mandatory`
- `scroll-snap-align:start`
- next-card peek
- scrollbar may be visually hidden
- no arrows/dots/JS unless the product requires explicit carousel controls

Ensure all cards are equal outer height when they belong to the same visual group. If a dynamic item is hidden, the remaining card(s) must not leave empty track space.

## Pattern: compact ecommerce product card

Use for narrow mobile product directories when the desktop card is too tall or control-heavy.

Recommended hierarchy:

1. small product/category label
2. product name
3. large contained product visual
4. footer row: price left, primary compact cart action right

Preserve PDP access via card/title/image link. For icon-only cart action, show a 24-28px icon but keep the actual clickable button about 44-48px.

Do not remove core product information from the data model merely to simplify mobile; hide presentation-only copy with scoped responsive CSS when appropriate.

## Pattern: editorial horizontal card

Use a full-width outer card with:

- metadata row: date left, category right
- body grid: thumbnail + content
- title 15-18px on small screens, usually 600 weight
- optional excerpt limited to 1-3 lines depending on density

Use `minmax(0,1fr)` for the text column. Shrink the thumbnail modestly at <=479px rather than collapsing the card back to a poor 2-column listing.

## Pattern: mobile timeline

Convert decorative desktop alternation into sequential reading:

`rail/node | year/title + description`

- rail 2px, visually light
- node 12-14px
- content aligned left
- natural item height
- 26-32px item spacing
- no desktop `right` alignment inherited on mobile

## Pattern: mobile nested menu

For parent items with children:

- tapping parent row opens submenu
- prevent immediate route navigation on the disclosure action
- first submenu item can be `[Parent] Overview` using the parent URL
- render child links dynamically from Shopify Navigation
- do not maintain a second hard-coded mobile menu tree

## Pattern: footer accordion

Use native `details/summary` for menu groups.

Default collapsed state:
- only parent rows visible
- 52-56px row height is a good starting point
- parent weight around 600
- one separator between groups, no redundant outer separator
- compact top/bottom container spacing

Expanded state:
- child links 44px+ touch area
- modest indentation
- 10-18px bottom spacing after children
- multiple groups may remain open unless product requirements say otherwise

## Pattern: responsive video

First validate rendering layers:

1. setting/source exists
2. embed/video element generated
3. wrapper has width + aspect ratio
4. desktop browser loads
5. mobile Safari/Chrome loads
6. in-app browser loads

If standard browsers work but an in-app browser fails, do not call it a CSS defect. Keep a provider link fallback and consider Shopify-hosted media for critical acquisition traffic.

## Pattern: equal-height sibling cards

Prefer:

- parent `display:grid` or flex with `align-items:stretch`
- card `display:flex; flex-direction:column`
- flexible body
- CTA/footer `margin-top:auto` when bottom alignment is desired

Avoid:
- JavaScript height measurement
- fixed card height chosen only to force equality
- huge `min-height` that creates blank areas

## Pattern: inline Theme Editor size override

If markup emits inline font size from a range setting and mobile CSS must cap it, do not delete the setting. Add a component-scoped mobile ceiling with enough precedence, using `!important` only when needed to beat the inline declaration.

Keep the desktop configured value untouched.

## Pattern: full-bleed background, constrained content

Separate outer visual width from content width:

- section background may be full viewport width
- inner content uses container/gutters
- avoid double negative margins/nested viewport widths that cause 320px overflow

## Pattern: responsive image sizing

After every layout change, revisit `sizes`:

- single-column mobile image: roughly viewport/container width
- 2-column mobile image: roughly half available width
- 3-column compact image: roughly one third
- horizontal card thumbnail: fixed/limited thumbnail width rather than full card width

Do not leave `sizes="92vw"` after converting a component to a 100px thumbnail.
