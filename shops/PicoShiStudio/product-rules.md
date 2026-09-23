# PicoShiStudio — Product Rules

## Highest Priority: Hanger Product Accuracy Lock

For all wooden hanger images, the real product photos supplied by the user are the structural source of truth.

AI MUST NOT change:

- Overall hanger silhouette
- Shoulder curve
- Shoulder width
- Shoulder thickness
- Overall width
- Overall height
- Lower trouser-bar position
- Lower trouser-bar thickness
- Lower trouser-bar connection
- Hook shape
- Hook length
- Hook angle
- Hook color
- Hook connection position
- Wood color
- Wood grain direction
- Wood texture density
- Surface finish character
- Structural joints
- Any existing hardware

AI MUST NOT:

- Make the hanger thicker to look more premium
- Make the shoulder rounder or wider than the real product
- Replace the real wood appearance with walnut, oak, beech, maple, or another named wood species unless Product Facts confirm it
- Add clips, notches, rubber strips, extra bars, branding, or hardware that the real product does not have
- Remove real structural features
- Change dimensions for visual balance

AI MAY change:

- Background
- Room / closet environment
- Lighting
- Camera angle
- Composition
- Supporting garments
- Non-product props

## SKU Isolation Rule

Every new product must start with a fresh Product Facts block.

The current SKU's Product Facts override all older products and all template examples.

Never inherit a previous SKU's:
- width
- height
- shoulder thickness
- wood species
- hook material
- color
- set quantity
- finish
- capacity

If the current SKU provides 44 × 25 cm with 5.5 cm shoulder thickness, then every image and listing for that SKU must use exactly those dimensions even if an older template example contains 44.5 × 25 cm / 4.5 cm.

Unknown = TBD.

## Execution Mode Upgrade

### Product-truth images
For IMAGE 02 / 03 / 04 / 05, default to **reference-preserving edit mode**, not free re-generation.

The real product itself should be preserved as much as possible. Preferred operations:
- remove / replace background
- crop
- rotate
- reframe
- duplicate the same real hanger
- arrange multiple copies
- add measurement arrows
- create close-up crops
- compose 2×2 details from the same real product

Do not redraw the hanger from scratch unless unavoidable.

### Lifestyle images
For IMAGE 01 / 06 / 07, AI may generate a new scene, but the hanger must remain structurally locked to the real reference.

### One image = one function
Never let:
- PRODUCT VIEW become a lifestyle scene
- SIZE GUIDE become a collage
- QUALITY DETAILS become a wardrobe scene
- CLOSET STYLING become a close-up product shot

Each slot must satisfy its assigned function before approval.

## Pre-generation Checklist

Before every image-generation call, restate internally:
1. Shop = PicoShiStudio
2. Current SKU = only the current uploaded product
3. Current Product Facts = current SKU only
4. Exact image function = one slot only
5. Required number of hangers
6. Required camera angle
7. Required background / scene
8. Forbidden content
9. Product structure lock
10. Output = 1:1 unless otherwise requested

## Post-generation Approval Gate

Reject and regenerate if any of the following is wrong:
- wrong number of hangers
- wrong template function
- wrong dimensions
- wrong shoulder thickness
- altered shoulder curve
- altered lower bar
- altered hook
- altered wood color / grain
- impossible hanger / garment placement
- merged or duplicated hardware
- unexpected collage
- unexpected text / numbering
- wrong scene type

Do not continue to the next image until the current image passes the approval gate.

## Product Facts Rule

Only use confirmed facts for:
- Wood species
- Hook material
- Surface coating / finish
- Weight capacity
- Sales quantity / set size
- Care instructions
- Manufacturing method
- Sustainability claims

Unknown = TBD.
