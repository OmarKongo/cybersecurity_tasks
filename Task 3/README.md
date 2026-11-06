# Véro Theme — AI-Assisted Development Guide (Simplified)

> Edit the Véro theme using Claude Code / Codex. Export → Local Playground → Test → Upload via WP Admin.

---

## Prerequisites (macOS)

```bash
# Install once
brew install node unzip
# Node gives you npx for WP Playground
```

---

## PHP Stubs for WordPress & WooCommerce (IDE Support)

**macOS:** Install Composer first if not present:
```bash
brew install composer
```

Install the stubs in your project folder (not inside the theme folder you upload):

```bash
composer require --dev php-stubs/wordpress-stubs php-stubs/woocommerce-stubs
```

In VS Code, make sure Intelephense can see them. It indexes the workspace, so if the `vendor/` folder is inside the opened folder, it usually picks them up. If it doesn't, add this to your VS Code settings:

```json
"intelephense.environment.includePaths": [
  "vendor/php-stubs/wordpress-stubs",
  "vendor/php-stubs/woocommerce-stubs"
]
```

---

## 1. Export Theme from Production

**WP Admin → Tools → Export → Theme** (your export plugin handles this)

Download `vero.zip` to your Mac.

---

## 2. Unzip & Set Up Local Folder

```bash
mkdir -p ~/vero-dev && cd ~/vero-dev
unzip -q vero.zip
# You now have: ~/vero-dev/vero/
```

**Create `blueprint.json` inside `vero/`** (required for WP Playground):

```bash
cat > vero/blueprint.json <<'EOF'
{
  "$schema": "https://playground.wordpress.net/blueprint-schema.json",
  "steps": [
    { "step": "defineWpConfigConsts", "consts": { "WP_DEBUG": true, "WP_DEBUG_DISPLAY": true } },
    { "step": "installPlugin", "pluginData": { "resource": "wordpress.org/plugins", "slug": "woocommerce" } }
  ]
}
EOF
```

**Read the architecture docs** (in `~/vero-dev/`):
- `vero-theme-architecture.md` — File flow, data pipeline, edit map
- `vero-theme-analysis.md` — Complete codebase breakdown

---

## 3. Export Products (CSV) — GUI Only

**WP Admin → WooCommerce → Products → Export → Generate CSV → Download**

Save as `~/vero-dev/products-export.csv`

---

## 4. Local Testing with WP Playground

**Why Playground?** Instant WordPress in browser — no Docker, no MySQL, no config. Runs entirely in your tab.

Start Playground from inside the theme folder as a local server:

```bash
cd ~/vero-dev/vero
npx @wp-playground/cli@latest server --auto-mount --blueprint=../blueprint.json --port=9400
```

- Runs at **http://localhost:9400** with Véro + WooCommerce pre-installed
- Theme is mounted live from `~/vero-dev/vero/` — edits reflect on refresh
- **Login:** `admin` / `password`

> **Note**: Flag names are from memory — check the current [Playground CLI docs](https://github.com/WordPress/playground/blob/main/docs/cli.md) if it complains.

**Import products in Playground:**
1. WP Admin → WooCommerce → Products → Import → Choose `products-export.csv` → Run

---

## 5. Verify Everything Works (in Playground)

| Page | Check |
|------|-------|
| `/` | Hero, Look carousel, Winter grid, Spotlight, Info, Still, Summer |
| `/shop/` | Knit tiles, Group filters, Product grid |
| `/product/<slug>/` | Images, color chips, size sheet, sticky buy bar |
| `/cart/` | Lines, steppers, totals, checkout link |
| `/checkout/` | Form loads |
| Mobile (<900px) | Tab bar, menu/search/size-guide sheets |

**Browser Console:** No JS errors. `VERO_CFG`, `#pdp-data`, `#look-data`, `#vero-products` present.

---

## 6. Making Changes (AI-Assisted)

```bash
cd ~/vero-dev/vero
claude  # or codex
```

**Ask Claude/Codex things like:**
- "Change 'Men' to 'Man' in navbar"
- "Change primary color to #2d5a3d"
- "Add new knit style 'Rib'"
- "Move size guide trigger to product page header"

**Key files by change type:**

| Change | Files |
|--------|-------|
| Text/Nav labels | `header.php`, `footer.php`, `archive-product.php` |
| Colors/Fonts/Spacing | `assets/css/vero.css:3-24` (design tokens) |
| Add knit style | `inc/products.php:8-14, 79-90, 214` |
| Add size chart | `inc/products.php:21-61, 64-77` |
| Home layout | `front-page.php` |
| Product layout | `woocommerce/single-product.php` |
| Shop filters | `archive-product.php` + `assets/js/vero.js:147-172` |
| Cart behavior | `page-cart.php` + `assets/js/vero.js:225-277` |

**Test in Playground:** Refresh browser after each edit.

---

## 7. Deploy to Production

```bash
cd ~/vero-dev
zip -r vero-v1.0.6.zip vero/ -x "*/.DS_Store"
```

**WP Admin → Appearance → Themes → Add New → Upload Theme → Choose `vero-v1.0.6.zip` → Activate**

Done.

---

## Quick Architecture Reference

```
functions.php (Orchestrator)
    │
    ├── require 'inc/products.php' (Data Engine)
    │       ├── vero_all_products() → cached 10min
    │       ├── vero_product_view() → normalized view-model
    │       ├── vero_sorted_products() → winter/rest split
    │       ├── vero_knits() → cable/velvet/zipup definitions
    │       ├── vero_size_charts() → 9 hardcoded chart IDs
    │       └── Components: vero_card, vero_chart_html, vero_size_sheet, vero_search_data
    │
    ├── Assets: vero.css → woo.css → vero.js (Client Brain)
    │
    └── Templates consume Data Engine:
        front-page.php     → vero_sorted_products(), vero_knits(), vero_card(), vero_chart_html(), vero_size_sheet()
        archive-product.php→ query IDs + vero_sorted_products() filtered, vero_knits() for tiles
        single-product.php → vero_product_view(), finds twin, vero_chart_html(), vero_size_sheet()
        page-cart.php      → Shell only, JS fetches Store API
```

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Styles missing | WP Admin → Appearance → Themes → Activate Véro |
| Cart empty | WC → Settings → Advanced → Enable Store API |
| Size guide empty | Verify `vero_size_charts()` chart IDs match products |
| Filters broken | Check `archive-product.php` data-attrs match `vero.js` selectors |
| JS errors | Console → usually missing `#vero-products` or `#pdp-data` JSON |

---

*Véro v1.0.5 — Bump version in `style.css` and `functions.php:VERO_VERSION` on release.*
