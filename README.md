# SHOP.CO — Growmodo Shopify Developer Assessment

**Candidate:** John Paul Guisijan
**Store:** growmodo-2.myshopify.com
**Theme ID:** 151372693643
**Base Theme:** Dawn (Shopify OS 2.0)
**Design Reference:** SHOP.CO Figma Community Template

---

## Overview

This project is a custom Shopify theme built on top of the Dawn base theme, faithfully implementing the SHOP.CO e-commerce design from Figma. All custom sections are prefixed `shopco-` to avoid conflicts with Dawn's native components.

---

## What Was Built

### 1. Homepage Sections

**Hero Banner** (`sections/shopco-hero.liquid`)
- Full-width banner with headline, subheadline, and CTA button
- Configurable image, text, and button via the Theme Editor
- Matches Figma layout with stat counters (200+ brands, 2000+ products, 30,000+ customers)

**New Arrivals / Featured Products** (`sections/shopco-products.liquid`)
- 4-column product grid with product cards
- Each card shows image, title, star rating, price, and discount badge
- Links to collection for "View All" CTA

**Browse by Style** (`sections/shopco-browse-style.liquid`)
- 2×2 equal-column CSS Grid layout (`grid-template-columns: 1fr 1fr`)
- Each card uses `aspect-ratio: 3/2` with absolute-positioned image for consistent sizing
- Labels overlay the image (top-left, bold)
- Up to 4 blocks, each with image picker, label, and link — all configurable in Theme Editor

**Top Selling / On Sale Collections** (`sections/shopco-products.liquid`)
- Reused product grid section targeting different collections

**Newsletter / Announcement Banner** (`sections/announcement-bar.liquid`)
- Promotional strip at top: "Sign up and get 20% off your first order"

### 2. Product Page (`sections/shopco-product.liquid`)

Custom product page replacing Dawns default, featuring:

- **Image gallery** — vertical thumbnail strip + large main image with click-to-switch
- **Breadcrumb navigation** — Home › Collection › Product
- **Variant selection** — Color swatches and size chips with active state highlighting
- **Quantity selector** — +/− buttons with input validation
- **AJAX Add to Cart** — Fetches `/cart/add.js` with JSON body; shows inline success/error messages without page redirect; updates cart count bubble in header
- **Price updates** — Price, compare-at price, and discount badge update dynamically on variant change
- **Tabs** — Product Details, Rating & Reviews (with sample reviews), FAQs (accordion)
- **You Might Also Like** — Pulls 4 related products from the same collection

### 3. Collection Page (`sections/shopco-collection.liquid`)

- Responsive product grid with filter/sort bar
- Breadcrumb, product count, and "View All" pagination link
- Product cards consistent with homepage cards

### 4. Custom Cart Page (`sections/shopco-cart.liquid` + `templates/cart.json`)

Replaced Dawn's default cart with a fully custom two-column layout:

- **Left column:** Cart items list with product image, name, variant options, quantity +/−, remove button, and line price — all updated via AJAX (`/cart/change.js`) without page redirect
- **Right column:** Order Summary with subtotal, discount (if any), delivery (Free), and total
- **Promo code input** — UI with Apply button
- **Go to Checkout** button via Shopify `{% form 'cart', cart %}` native form
- **Empty state** with "Continue Shopping" link to `/collections/all`

### 5. Styling (`assets/shopco.css`)

All custom styles live in a single file to keep them isolated from Dawn's CSS:

- CSS custom properties for brand colors, typography, and radii
- Satoshi font via Google Fonts for headings
- Fully responsive — mobile breakpoints at 768px and 480px
- No external CSS frameworks used

---

## Technical Approach

- **Shopify OS 2.0 sections** — all custom sections use `{% schema %}` blocks for Theme Editor configurability
- **No theme replacement** — Dawn is kept intact; custom sections are additive
- **AJAX cart** — All cart interactions (add, update quantity, remove) use the Cart AJAX API (`/cart/add.js`, `/cart/change.js`, `/cart.js`) to avoid page reloads
- **Shopify CLI** used for all theme pushes: `shopify theme push --allow-live --theme 151372693643 --only <file>`
- **Liquid templating** — variant selection, image rendering, collection loops, and money formatting all done server-side in Liquid where possible

---

## File Structure (Custom Files)

```
assets/
  shopco.css              # All custom styles

sections/
  shopco-hero.liquid          # Hero banner
  shopco-products.liquid      # Product grid (homepage + collections)
  shopco-collection.liquid    # Collection page layout
  shopco-product.liquid       # Product detail page
  shopco-browse-style.liquid  # Browse by Style 2x2 grid
  shopco-cart.liquid          # Custom cart page

snippets/
  shopco-product-card.liquid  # Reusable product card snippet

templates/
  cart.json               # Routes cart page to shopco-cart section
  product.json            # Routes product page to shopco-product section
  collection.json         # Routes collection page to shopco-collection section
```

---

## Store Setup

- **Store name:** SHOP.CO
- **Navigation:** Shop, On Sale, New Arrivals, Brands
- **Collections:** Top Selling, New Arrivals, On Sale
- **Products:** Imported with images, variants (size/color), and pricing matching SHOP.CO Figma
- **Inventory:** Set to "Continue selling when out of stock" for all variants

---

## GitHub Repository

[https://github.com/johnpaulguisijan-png/Growmodo_assessment](https://github.com/johnpaulguisijan-png/Growmodo_assessment)
