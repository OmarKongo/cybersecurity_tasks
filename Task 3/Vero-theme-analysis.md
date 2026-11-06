# Véro Theme — Complete Codebase Analysis

> **Theme:** Véro (v1.0.5)  
> **Author:** Abdo Tamim  
> **Type:** Mobile-first WooCommerce theme for Véro knitwear  
> **Stack:** PHP 7.4+, WordPress 6.4+, WooCommerce 8.0+  
> **Key trait:** No Elementor on core pages — header, footer, home, shop, product, bag, 404 are native PHP templates. Elementor only on editor-built pages (checkout, account, policies).

---

## File Structure

```
vero/
├── style.css              # Theme metadata (styles in assets/css/)
├── functions.php          # Core logic: assets, cart, size charts, filters, templates
├── header.php             # Header + mobile menu drawer
├── footer.php             # Footer + tab bar + dialogs (menu, search, size guide)
├── front-page.php         # Home: hero, shop-the-look, winter grid, spotlight, info, still, summer
├── page.php               # Generic pages (checkout, account, policies) inside Véro layout
├── page-cart.php          # Bag page (Store API driven)
├── 404.php                # Not found
├── index.php              # Fallback: posts, archives, search
├── woocommerce/
│   ├── single-product.php # Product page (Merino)
│   └── archive-product.php# Shop + categories (Kiosk57 filters)
├── inc/
│   └── products.php       # Product view-model, size charts, sorting, cards, search index
└── assets/
    ├── css/
    │   ├── vero.css       # All theme CSS (design system, components, layouts)
    │   └── woo.css        # WooCommerce forms, checkout, account, notices
    └── js/
        └── vero.js        # Store API cart, sheets, filters, product page, bag page
```

---

## Design System (vero.css — `:root`)

| Token | Value | Purpose |
|-------|-------|---------|
| `--paper` | `#eeeae2` | Base background |
| `--paper-2` | `#e4ded3` | Alt background (cards, rows) |
| `--stone` | `#d6cfc1` | Subtle borders, placeholders |
| `--ink` | `#161b17` | Primary text |
| `--muted` | `#565c55` | Secondary text |
| `--green` | `#394b35` | Brand green (CTAs, links, focus) |
| `--deep` | `#1b3022` | Dark sections (spotlight) |
| `--cream` | `#f0e1c3` | Accent on dark |
| `--fabric` | `#2c3722` | Darker green |
| `--band` | `#0f0f0e` | Tab bar background |
| `--line` | `rgba(22,27,23,.14)` | Borders, dividers |
| `--sale` | `#7a2a1f` | Sale/error red |
| `--r` | `28px` | Border radius (cards, media) |
| `--gut` | `16px` (32px desktop) | Page gutter |
| `--tab` | `58px` | Tab bar height |
| `--ui` | `Archivo` | UI font (variable width/weight) |
| `--serif` | `Cormorant Garamond` | Display/editorial font |
| `--pixel` | `Pixelify Sans` | Monospace accent |
| `--ease` | `cubic-bezier(.2,.7,.2,1)` | Standard transition |

**Fonts loaded:** Archivo (variable), Cormorant Garamond (italic 400/500), Pixelify Sans (400)

---

## Core Architecture Concepts

### 1. **Page Ownership Model** (`functions.php:53-55`)
```php
function vero_is_own_page() {
    return is_front_page() || is_shop() || is_product_taxonomy() || is_product() || is_cart() || is_404();
}
```
- **Own pages** (theme controls everything): Home, Shop, Category, Product, Bag, 404
- **Editor pages** (Elementor/plugins allowed): Checkout, My Account, Policies, custom pages
- On own pages, `vero_strip_assets()` dequeues Elementor, Essential Addons, Header-Footer-Elementor, Swiper, widget scripts, jQuery UI, WooCommerce jQuery add-to-cart, single-product scripts, swatches, block library, Photoswipe, dashicons.

### 2. **Store API Cart** (No jQuery, no fragments)
- Cart data via `wc/store/v1/cart` (GET) and `wc/store/v1/cart/add-item` (POST)
- Nonce auto-refreshed from response headers
- Works on cached pages — JS fetches fresh cart on load
- `vero_cart_count()` prints server count (for initial render), JS corrects it

### 3. **Product View-Model** (`inc/products.php:106-191`)
`vero_product_view($product)` → normalized array used by **all templates + JS**:
```php
[
  'id', 'slug', 'link', 'name', 'gender', 'season', 'cat',
  'style', 'knit', 'chart', 'price', 'regular', 'inStock',
  'sizes', 'colors', 'color', 'hex', 'imageId', 'img', 'images', 'vars'
]
```
- Cached 10 min (`vero_products_v3` transient), invalidated on product save/stock change
- `vero_all_products()` → all published products as view-models
- `vero_sorted_products()` → `[winter[], rest[]]` — winter first (women→men, cable→velvet→zipup), then rest (in-stock first)

### 4. **Three Design "Systems" in One Theme**

| System | Pages | Key Files |
|--------|-------|-----------|
| **Halcy** | Home (hero, look, grid, info, still) | `front-page.php`, `vero.css:.hero`, `.look`, `.grid`, `.info`, `.still` |
| **Kiosk57** | Header, tab bar, shop filters | `header.php`, `footer.php`, `archive-product.php`, `vero.css:.hdr`, `.tabs`, `.cats`, `.seg` |
| **Merino** | Product page | `woocommerce/single-product.php`, `vero.css:.pdp`, `.buy` |
| **Pearl-Art** | Spotlight section | `front-page.php`, `vero.css:.spot` |
| **Knitwear Stillife** | Still life section | `front-page.php`, `vero.css:.still` |
| **KAPUSTA** | Identity rows (footer area) | `front-page.php`, `vero.css:.ident`, `.rows` |

---

## Template Breakdown

### `header.php` — Sticky Header + Mobile Menu Button
- **Grid:** `[Menu btn] [Logo] [Nav links | Search + Bag]`
- **Nav links (desktop only):** Winter 2027, Summer 2026, Women, **Men** ← *change target here*
- **Mobile:** Menu button opens `#menu` dialog (in footer)
- **Sticky:** `.is-stuck` class on scroll > 8px (border appears)
- **Preload:** Hero image on home page

### `footer.php` — Footer + Fixed Tab Bar + All Dialogs
- **Footer nav:** Shop, Size guide, Shipping, Instagram, Terms, Privacy, Account
- **Tab bar (mobile):** Home, Shop, Search, Bag, Account — fixed bottom, hides on product pages
- **Dialogs (all here, not in header):**
  - `#menu` — full nav with Shop all, seasons, Women, **Men**, Size guide, Shipping, Instagram
  - `#search` — live product search (JS filters `vero-products` JSON)
  - `#size-guide` — size sheet with cable/velvet/summer charts (no buttons, all charts shown)
- **JSON data:** `vero-products` (search index), `pdp-data` (product page), `look-data` (shop the look)

### `front-page.php` — Home Page (Halcy)
**Sections in order:**
1. **Hero** — full-screen group photo, headline "Three knits, worn by two.", CTA → Winter 2027
2. **Shop the Look** — carousel of 3 pieces (cable Women, velvet Men, zipup Men), size sheet per piece
3. **Most Worn (Winter)** — grid of winter products (women→men, cable→velvet→zipup)
4. **Spotlight (Pearl-Art)** — Zip-Up hero with texture callout, "Also for men" link
5. **Info Card** — "One chart, both of you" — fit philosophy + stats
6. **Still Life** — folded knits photo, "The winter three." + price
7. **Summer 2026** — hero image + 4 in-stock summer products

**Data flow:** `vero_sorted_products()` → filters by style/gender → builds `$look` array with color/size alternates

### `woocommerce/single-product.php` — Product Page (Merino)
**Layout:** Sticky top bar (back, logo, bag) → Media card (main image, color chips, price, texture callout, pager) → Thumbs → Body (description, facts, size guide button, sticky buy bar)
**Sticky buy bar (mobile):** `[Size] [ADD TO BAG] [Qty]` — fixed bottom, hides tab bar
**Size sheet:** Dialog with size buttons + actual chart for this product's knit
**Qty sheet:** Dialog with ± buttons (1–9)
**Related:** "Wear it with" grid (4 in-stock from same season or rest)

### `woocommerce/archive-product.php` — Shop / Category (Kiosk57)
**Filters (two rows):**
1. **Knit tiles (`.cats`)** — visual buttons for Cable, Velvet, Zip-Up (images from `vero_knits()`)
2. **Segmented controls (`.seg`)** — All, Women, Men, Winter 27, Summer 26, In stock
**Grid:** 2-col mobile, 4-col desktop — `vero_card()` markup
**URL state:** Hash-based `#style+group` for deep linking / browser back

### `page-cart.php` — Bag Page
- **Server-rendered shell only** — JS populates from Store API
- **Line items:** Image, name, options, line total, stepper (−/qty/+), Remove
- **Summary:** Subtotal, Discount, Shipping, Total, Checkout button
- **Empty state:** "Your bag is empty" + Shop Winter 2027 link

### `page.php` — Editor Pages (Checkout, Account, Policies)
- Gets Véro header/footer/layout
- Content in `.woo-page` (checkout) or `.policy` (policies)
- Wide layout for checkout/account, narrow for policies

---

## Size Chart System (`inc/products.php:21-61`)

**Three charts, typed from chart images:**
| Key | Label | Use Case | Both Genders? |
|-----|-------|----------|---------------|
| `cable` | Cable Knit & Zip-Up | Cable knit + Zip-Up (both genders) | ✅ |
| `velvet` | Velvet Knit | Velvet knit (both genders) | ✅ |
| `summer` | Summer tops | Summer women's tops | ❌ |

**Chart data structure:**
```php
'cols' => ['Size', 'Bust (width)', 'Waist', 'Length', 'Shoulder'],
'rows' => [['Small','S','56–58','58–60','60','57–59'], ...],
'note' => 'Measurements are taken flat, in cm...',
'models' => [['Model (female)','168 cm · 57 kg · wears S'], ['Model (male)','179 cm · 73 kg · wears M']],
'both' => true/false
```

**Product → chart mapping:** `vero_chart_key($product_id, $style)` — hardcoded IDs first, then style fallback

**Rendering:** `vero_chart_html($key, $hidden, $titled)` → `<table>` + note + models
**Size sheet dialog:** `vero_size_sheet($id, $sizes, $in_stock, $charts[], $buttons)`
- With buttons (product page, shop the look): one chart at a time, switched by size
- Without buttons (size guide): all charts, each with title

---

## JavaScript Architecture (`assets/js/vero.js`)

**Single IIFE, no dependencies.** Key modules:

| Module | Responsibility |
|--------|----------------|
| **Store API** | `api()`, `getCart()`, `add()` — nonce handling, variation matching |
| **Bag count** | `paintCount()` — updates all `[data-bag-count]` elements |
| **Sheets** | `dialog.sheet` open/close, click backdrop to close, `[data-open]` triggers |
| **Header scroll** | `.is-stuck` on `.hdr` / `.pdp-bar` |
| **Search** | Live filter `vero-products` JSON → `#results` |
| **Size pickers** | Shared `pick(wrap, onPick)` for size buttons in sheets |
| **Home: Shop the Look** | Carousel (thumbs + arrows + swipe), per-piece size sheet, add to bag |
| **Shop filters** | Knit style + group filters, hash state, live count |
| **Product page** | Image pager/thumbs/swipe, color chips, size sheet, qty sheet, add to bag |
| **Bag page** | Load cart, render lines, stepper/remove via API, totals |

**Variation matching** (lines 35-37):
```js
const variationFor = (vars, size, color) => vars.find(v =>
  (!v.size || same(v.size, size)) && (!color || !v.color || same(v.color, color)) && v.inStock
);
```

---

## Crucial Points & Gotchas

### 1. **"Men" → "Man" Change Locations**
The navbar "Men" label appears in **three places** (all hardcoded in templates):
| File | Line | Context |
|------|------|---------|
| `header.php` | 19 | Desktop header nav: `<a href="...men...">Men</a>` |
| `footer.php` | 37 | Mobile menu drawer: `<a href="...men...">Men <span></span></a>` |
| `archive-product.php` | 24 | Filter button: `'men' => 'Men'` |

**Also in PHP logic:** `inc/products.php:113` — gender detection from category slug `'women'` → `'Women'` else `'Men'`. If you change the category slug, update here.

### 2. **No Elementor on Core Pages**
- Home, Shop, Category, Product, Bag, 404 are **native PHP**
- Elementor assets aggressively dequeued on these pages (`vero_strip_assets()`)
- Only Checkout, My Account, Policies, custom pages use Elementor

### 3. **CSS Load Order**
```php
wp_enqueue_style( 'vero-fonts', 'https://fonts.googleapis.com/...' );
wp_enqueue_style( 'vero', 'assets/css/vero.css', ['vero-fonts'] );
wp_enqueue_style( 'vero-woo', 'assets/css/woo.css', ['vero'] );
```
- `vero.css` = entire design system + all components
- `woo.css` = WooCommerce forms, checkout, account, notices only

### 4. **WooCommerce Styles Fully Disabled**
```php
add_filter( 'woocommerce_enqueue_styles', '__return_empty_array' );
wp_dequeue_style( 'wc-blocks-style' );
```
- Theme provides **all** WooCommerce styling (forms, checkout, blocks)
- Block cart/checkout also styled in `woo.css`

### 5. **Product Grid = 2 Col Mobile, 4 Col Desktop**
```css
.grid { grid-template-columns: repeat(2, 1fr); }
@media (min-width: 900px) { .grid { grid-template-columns: repeat(4, 1fr); } }
```
- 48 products per page (`loop_shop_per_page` → 48)

### 6. **Cart Page Override**
```php
add_filter( 'template_include', function($template) {
    if (is_cart()) return locate_template('page-cart.php');
}, 99);
```
- Any "Cart" page slug uses `page-cart.php` (Store API bag)

### 7. **Structured Data on Product Pages**
```php
add_action( 'vero_product_schema', function() {
    if (isset(WC()->structured_data)) WC()->structured_data->generate_product_data();
});
```
- Called in `single-product.php` after template — keeps WooCommerce JSON-LD

### 8. **Preconnect + Hero Preload**
```php
add_filter('wp_resource_hints', ...); // fonts.googleapis.com, fonts.gstatic.com
add_action('wp_head', ...); // preload hero-group.webp on home
```

### 9. **Theme Color Meta**
```php
add_action('wp_head', function() {
    echo '<meta name="theme-color" content="#394b35">';
});
```

### 10. **Body Class for Product Pages**
```php
add_filter('body_class', function($c) {
    if (is_product()) $c[] = 'has-buy';
    return $c;
});
```
- Enables sticky buy bar CSS (`body.has-buy { padding-bottom: ...; }`)

---

## Key Functions Reference

| Function | File | Purpose |
|----------|------|---------|
| `vero_asset($path)` | `functions.php:22` | `get_theme_file_uri('assets/' . $path)` |
| `vero_is_own_page()` | `functions.php:53` | True for theme-owned pages |
| `vero_strip_assets()` | `functions.php:56` | Dequeue Elementor/WC scripts on own pages |
| `vero_cart_count()` | `functions.php:123` | Server-side cart count |
| `vero_page_url($path)` | `functions.php:128` | Page URL by path, fallback to home |
| `vero_cat_url($slug)` | `functions.php:133` | Product category URL by slug |
| `vero_icon($name)` | `functions.php:138` | Inline SVG icons (back, bag, arrow, x) |
| `vero_chart_html($key, $hidden, $titled)` | `functions.php:149` | Render size chart table |
| `vero_size_sheet($id, $sizes, $in_stock, $charts[], $buttons)` | `functions.php:178` | Size guide dialog markup |
| `vero_knits()` | `inc/products.php:8` | Knit style definitions (label, color, hex, cut, texture, desc) |
| `vero_size_charts()` | `inc/products.php:21` | Three size charts (cable, velvet, summer) |
| `vero_chart_key($product_id, $style)` | `inc/products.php:64` | Product ID → chart key mapping |
| `vero_style_of($name)` | `inc/products.php:79` | Product name → style key (cable/velvet/zipup/other) |
| `vero_color_hex($name)` | `inc/products.php:92` | Color name → hex map |
| `vero_money($amount)` | `inc/products.php:98` | Format EGP with commas |
| `vero_product_view($product)` | `inc/products.php:106` | WC_Product → normalized view-model |
| `vero_all_products()` | `inc/products.php:194` | All products as view-models (cached 10 min) |
| `vero_sorted_products()` | `inc/products.php:214` | `[winter[], rest[]]` sorted |
| `vero_card($p, $eager)` | `inc/products.php:230` | Product card markup (Halcy grid) |
| `vero_search_data()` | `inc/products.php:267` | Compact array for search sheet JSON |

---

## Asset Dependencies

| Asset | Dependencies | Version |
|-------|--------------|---------|
| `vero-fonts` | — | null |
| `vero` (vero.css) | `vero-fonts` | `VERO_VERSION` |
| `vero-woo` (woo.css) | `vero` | `VERO_VERSION` |
| `vero` (vero.js) | — | `VERO_VERSION` (defer, in_footer) |

**Localized JS config (`VERO_CFG`):**
```js
{
  store: rest_url('wc/store/v1/'),
  nonce: wp_create_nonce('wc_store_api'),
  cart: wc_get_cart_url(),
  checkout: wc_get_checkout_url(),
  placeholder: wc_placeholder_img_src('woocommerce_thumbnail')
}
```

---

## Customization Guide

### Change "Men" → "Man" (3 edits)
1. `header.php:19` — `<a href="...">Men</a>` → `<a href="...">Man</a>`
2. `footer.php:37` — `<a href="...">Men <span></span></a>` → `<a href="...">Man <span></span></a>`
3. `archive-product.php:24` — `'men' => 'Men'` → `'men' => 'Man'`

**Also consider:** Category slug `men` in WP Admin → Products → Categories. If changed, update `inc/products.php:113` gender detection.

### Add a New Knit Style
1. `inc/products.php:8-14` — add to `vero_knits()`
2. `inc/products.php:79-90` — add detection in `vero_style_of()`
3. `inc/products.php:214` — add to `$order` in `vero_sorted_products()`
4. `archive-product.php:33-35` — knit tile button uses `vero_knits()` automatically

### Add a Size Chart
1. `inc/products.php:21-61` — add to `vero_size_charts()`
2. `inc/products.php:64-77` — add to `vero_chart_key()` mapping
3. Product edit → set correct category/tag for chart assignment

### Modify Colors
Edit CSS custom properties in `vero.css:3-24` — all components use tokens.

### Change Fonts
1. `functions.php:27` — update Google Fonts URL
2. `vero.css:19-21` — update `--ui`, `--serif`, `--pixel`

---

## Performance Notes

- **CSS:** Single `vero.css` (all components), `woo.css` (WC only) — no per-page splitting
- **JS:** Single `vero.js` (defer) — ~8KB gzipped
- **Images:** WebP throughout (`hero-group.webp`, `cut-*.webp`, `IMG_*.webp`)
- **Preload:** Hero image on home (`wp_head` action)
- **Preconnect:** Google Fonts origins
- **Product data:** Cached 10 min via transient (`vero_products_v3`)
- **Cart:** Store API — no AJAX fragments, works on cached pages

---

## Dependencies

| Plugin | Required | Purpose |
|--------|----------|---------|
| WooCommerce | ✅ 8.0+ | Products, cart, checkout, Store API |
| Elementor | Optional | Editor pages only (checkout, account, policies) |
| Essential Addons | Optional | Widgets on editor pages |
| Header Footer Elementor | Optional | Header/footer on editor pages |

**Theme declares:** `Requires Plugins: woocommerce`

---

## File Ownership Map

| Feature | Template | CSS Section | JS Module |
|---------|----------|-------------|-----------|
| Header | `header.php` | `.hdr` | Header scroll |
| Footer | `footer.php` | `.foot` | — |
| Tab bar | `footer.php` | `.tabs` | — |
| Mobile menu | `footer.php` (#menu) | `.menu-links` | Sheets |
| Search | `footer.php` (#search) | `.search-in`, `.results` | Search |
| Size guide | `footer.php` (#size-guide) | `.sheet`, `.st` | Sheets |
| Hero | `front-page.php` | `.hero` | — |
| Shop the look | `front-page.php` | `.look`, `.look-stage` | Shop the look |
| Winter grid | `front-page.php` | `.grid`, `.card` | — |
| Spotlight | `front-page.php` | `.spot` | — |
| Info card | `front-page.php` | `.info`, `.info-card` | — |
| Still life | `front-page.php` | `.still` | — |
| Summer | `front-page.php` | `.summer` | — |
| Shop/Category | `archive-product.php` | `.cats`, `.seg`, `.grid` | Shop filters |
| Product page | `single-product.php` | `.pdp`, `.buy` | Product page |
| Bag page | `page-cart.php` | `.bag-list`, `.sum` | Bag page |
| Checkout/Account | `page.php` | `.woo-page` | (WC blocks) |
| Policies | `page.php` | `.policy` | — |
| 404 | `404.php` | `.empty` | — |

---

## Version History (from style.css)
- **1.0.5** — Current
- Requires WP 6.4+, PHP 7.4+, WC 8.0+
- Tested up to WP 7.1, WC 11.2

---

*Generated from source analysis of `/home/kongo/shady/vero/` on 2026-11-05*
