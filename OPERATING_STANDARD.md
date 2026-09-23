# New-SHOP Operating Standard

> Purpose: Operating standard for managing many Etsy shops, reusable product-image templates, and reusable listing templates in one GitHub knowledge base.
>
> Core idea: **GitHub is the long-term knowledge/configuration center. ChatGPT conversations are execution windows. Templates are organized by product type, not by shop.**

---

# 1. Why this structure is needed

The business may eventually operate 40–50 Etsy shops.

If every shop has separate conversations for curtains, pillow covers, tablecloths, hangers, aprons, etc., the number of conversations becomes unmanageable.

The solution is:

1. Store long-term rules in GitHub.
2. Separate **shop configuration** from **product templates**.
3. Reuse one product template across many shops.
4. Use ChatGPT conversations mainly for current product execution.
5. Do not rely on a long conversation as the source of truth.

---

# 2. Core architecture

Recommended repository structure:

```text
New-SHOP/
│
├── README.md
├── OPERATING_STANDARD.md
│
├── shops/
│   ├── StellaGoodsGifts/
│   │   ├── shop-profile.md
│   │   ├── visual-style.md
│   │   ├── listing-style.md
│   │   └── product-rules.md
│   │
│   ├── Shop-002/
│   │   ├── shop-profile.md
│   │   ├── visual-style.md
│   │   ├── listing-style.md
│   │   └── product-rules.md
│   │
│   └── ...
│
├── templates/
│   ├── pillow-cover/
│   │   ├── image-template.md
│   │   └── listing-template.md
│   │
│   ├── curtain/
│   │   ├── image-template.md
│   │   └── listing-template.md
│   │
│   ├── wooden-hanger/
│   │   ├── image-template.md
│   │   └── listing-template.md
│   │
│   ├── tablecloth/
│   │   ├── image-template.md
│   │   └── listing-template.md
│   │
│   ├── apron/
│   │   ├── image-template.md
│   │   └── listing-template.md
│   │
│   └── ...
│
├── workflows/
│   ├── new-product-workflow.md
│   ├── image-production-workflow.md
│   └── listing-production-workflow.md
│
└── products/
    ├── StellaGoodsGifts/
    ├── Shop-002/
    └── ...
```

This is the target architecture. Individual folders/files can be created gradually as each shop and product category is developed.

---

# 3. Separate shop rules from product templates

This separation is mandatory.

## Shop configuration

A shop file describes the identity of one shop.

Examples:

- Brand positioning
- Target customer
- Visual tone
- Preferred room styling
- Preferred colors
- Main product categories
- Listing tone
- SEO direction
- Watermark rules
- Pricing / packaging rules when applicable
- Shop-specific restrictions

Example:

```text
shops/StellaGoodsGifts/shop-profile.md
```

## Product template

A product template describes how a category should be produced regardless of which shop uses it.

Examples:

- Pillow Cover 8-image template
- Curtain 8-image template
- Wooden Hanger 8-image template
- Tablecloth image template
- Apron listing template

Example:

```text
templates/wooden-hanger/image-template.md
```

### Important

Do not duplicate the entire hanger template inside 40 shop folders.

Write the hanger template once and let many shops reuse it.

---

# 4. Recommended ChatGPT conversation structure

Do **not** create one conversation for every shop × every template.

Instead, keep a limited number of conversations organized by product type.

Example long-term conversations:

- Pillow / Cushion Production
- Curtain Production
- Table Linen Production
- Wooden Hanger Production
- Apron Production
- Chair Cushion Production
- Sofa Textile Production
- General Listing / SEO
- Shop Branding / Positioning

A single Wooden Hanger conversation may serve many different shops.

The shop identity is loaded from GitHub at the beginning of a task.

---

# 5. Standard task header

At the start of every new product, explicitly provide or resolve:

```text
SHOP: StellaGoodsGifts
TEMPLATE: wooden-hanger
PRODUCT: new product
```

Then load:

```text
shops/StellaGoodsGifts/...
templates/wooden-hanger/...
```

and combine them with the current Product Facts.

Recommended execution context:

```text
Shop Configuration
+
Product Template
+
Current Product Facts
=
Current Product Production Rules
```

---

# 6. New-product execution rule

For every new product:

1. Identify the shop.
2. Identify the product-template category.
3. Read the shop configuration from GitHub.
4. Read the product image template from GitHub.
5. Read the product listing template from GitHub.
6. Read current Product Facts supplied by the user.
7. Do not inherit facts from the previous SKU.
8. Generate / edit product images.
9. Perform Product Accuracy Review.
10. Generate Etsy listing copy.
11. Save the final product record if requested.

---

# 7. Product Facts are always isolated by SKU

This is critical when many products are generated in one conversation.

For every new product, create a fresh Product Facts block.

Example:

```text
PRODUCT FACTS

Shop: StellaGoodsGifts
Category: Wooden Hanger

Material: TBD
Color: Natural Wood
Width: 44.5 cm
Height: 25 cm
Shoulder Width: 4.5 cm
Hook Material: TBD
Sales Unit: TBD
Care: TBD
```

Rules:

- Current Product Facts override previous product facts.
- Never copy a previous SKU's dimensions automatically.
- Never reuse a previous product's material simply because it looks similar.
- Never reuse a previous product's variation structure without confirmation.
- Unknown = TBD.

---

# 8. Avoid cross-template image-generation errors

When multiple templates exist, the image model may incorrectly associate:

- “Image 7”
- “Image 8”
- “template”
- “fullness”
- “lining”

with a previous category.

Therefore:

## User-facing workflow numbers are allowed

The user may say:

> Generate image 7.

## But the actual image-generation instruction should be converted internally into the exact functional task

Example:

Instead of:

```text
Generate Image 7 from the wooden hanger template.
```

use:

```text
Create one 1:1 macro product image of the natural wood hanger.
Show only the smooth wood grain, rounded shoulder surface,
polished edge, and wooden bar connection.
No closet scene.
No garments.
No curtains.
No collage.
No numbering.
No text unless explicitly required.
```

This greatly reduces template cross-contamination.

---

# 9. One image = one function

Every template image must have a distinct job.

Do not replace a required detail image with another lifestyle image.

Examples:

## Pillow Cover

- HERO = lifestyle
- FRONT VIEW = product truth
- FABRIC DETAIL = textile macro
- SIDE VIEW = product structure
- CONSTRUCTION = zipper / tassel / edge
- SECOND ROOM = second lifestyle scene
- SIZE GUIDE = factual dimensions
- SHOP THE LOOK = styling

## Wooden Hanger

- HERO = lifestyle / product introduction
- PRODUCT FRONT = clean product view
- SIZE GUIDE = dimensions
- WIDE SHOULDER DETAIL = shoulder construction
- QUALITY DETAILS = hook / wood / bar / finish
- IN USE = garments on hangers
- MATERIAL DETAIL = wood grain / surface
- CLOSET STYLING = organized closet scene

Do not let Image 7 of one category become Image 7 of another category.

---

# 10. Final image rules

Unless a category template explicitly says otherwise:

- Final Etsy images should normally be 1:1.
- Do not put internal workflow numbers on final images.
- Do not generate an 8-panel template overview when the request is for 8 separate final images.
- Product-truth images must prioritize accuracy.
- Lifestyle images may change scene/background but not product facts.
- Do not invent dimensions.
- Do not invent materials.
- Do not invent product features.
- Do not invent available options.
- Do not add nonexistent SKUs into Shop the Look.

---

# 11. Product Accuracy First

Global rule:

> **Product accuracy first. Scene styling second.**

AI may usually change:

- Scene
- Background
- Composition
- Lighting
- Camera distance
- Styling direction

AI should preserve:

- Product shape
- Product proportions
- Pattern
- Pattern scale
- Color
- Fabric appearance
- Hardware
- Tassels / fringe
- Piping
- Closure
- Dimensions
- Structural details

A beautiful but inaccurate image is rejected.

---

# 12. GitHub is the source of long-term memory

Do not depend on ChatGPT remembering hundreds of shops and templates from conversation history.

GitHub should hold:

- Shop profiles
- Visual rules
- Image templates
- Listing templates
- Product Facts
- Prompts
- Product status
- Listing copy
- SEO rules
- Workflow rules

ChatGPT conversations should primarily execute the current task.

---

# 13. Recommended invocation format

For a new product:

```text
Shop = StellaGoodsGifts
Template = wooden-hanger
New Product

Read the corresponding shop configuration and product template from New-SHOP.
Do not inherit facts from the previous SKU.
I will now provide source images and Product Facts.
```

For another shop using the same hanger template:

```text
Shop = Shop-017
Template = wooden-hanger
New Product
```

The same template is reused, while shop styling comes from the Shop-017 configuration.

---

# 14. Updating templates

When a template improves:

1. Update the shared template file.
2. Do not manually edit 40–50 shop copies.
3. All future products should use the newest approved template.
4. If a shop needs an exception, record the exception in the shop configuration.

Example:

Shared rule:

```text
templates/pillow-cover/image-template.md
```

Shop-specific exception:

```text
shops/StellaGoodsGifts/product-rules.md
```

This avoids duplicate maintenance.

---

# 15. Template versioning

As the system grows, add a simple version number.

Example:

```text
Template: pillow-cover
Version: 1.2
Updated: 2026-09-23
```

Product records may optionally store:

```text
Image Template Version: 1.2
Listing Template Version: 1.1
```

This makes it easier to know which rule set produced an older listing.

---

# 16. Recommended future build sequence

Do not build all 40–50 shops at once.

Build gradually:

### Step 1
Create shared templates when a new product category is first used.

### Step 2
Create a shop profile when a shop begins active production.

### Step 3
Create product records only for real products being processed.

### Step 4
Refine shared templates based on production experience.

This keeps the repository clean and practical.

---

# 17. Current New-SHOP direction

New-SHOP will act as the shared operations knowledge base for multiple Etsy shops.

Current confirmed shop document:

```text
StellaGoodsGifts.md
```

Going forward, StellaGoodsGifts content should gradually be migrated / expanded into:

```text
shops/StellaGoodsGifts/
```

Shared product templates should gradually move into:

```text
templates/
```

Existing useful information should not be deleted during migration.

---

# 18. Master operating principle

> **Do not organize knowledge around conversations. Organize it around reusable shop configuration + reusable product templates + current Product Facts.**

The operating model is:

```text
GitHub
= long-term knowledge and configuration

ChatGPT conversation
= current execution workspace

Shop configuration
= brand-specific rules

Product template
= category-specific production rules

Product Facts
= SKU-specific source of truth
```

This structure is designed to scale from a few shops to dozens of shops without requiring hundreds of separate conversations.
