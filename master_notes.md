ROLE
You are a senior front-end developer and UI designer. Build a complete, production-quality, multi-page static website for "Vasu Ettan Bakery" using ONLY plain HTML5, CSS3 and vanilla JavaScript (ES6+). No frameworks, no build tools, no backend, no npm dependencies. Google Fonts via <link> is allowed.

DESIGN DIRECTION
"Traditional Bakery Heritage × Premium Modern E-commerce." Elegant not flashy, warm not sterile. Handcrafted, authentic, rich, classic, trustworthy. Keep layouts minimal so product photos, typography and the logo are the focus. No decorative patterns behind every section; optional low-opacity parchment/wheat texture only in one or two selected sections.

PAGES AND ROUTES
index.html (Home), shop.html (Shop), about.html (About), blog.html (Blog list + article detail via ?slug=), plus reusable header.html and footer.html loaded into every page with fetch() and injected into placeholders (include a fallback note for opening via file:// and recommend running a local server such as VS Code Live Server).

FOLDER STRUCTURE (create exactly this)
vasu-ettan-bakery/
  index.html, shop.html, about.html, blog.html, header.html, footer.html, master_notes.md
  assets/images/ (logo.png, hero-bakery.webp, products/, about/, blog/), assets/icons/
  css/ (variables.css, style.css, responsive.css)
  js/ (main.js, products.js, cart.js, blog.js)
  data/ (products.json, combos.json, posts.json)

DESIGN TOKENS (css/variables.css, reuse everywhere, no hard-coded colors elsewhere)
:root {
  --color-chocolate:#35170F; --color-cocoa:#6B3821; --color-gold:#C79A42;
  --color-ivory:#F2E4C5; --color-cream:#FBF7EF; --color-wheat:#D8C7A4;
  --color-cinnamon:#75432D; --color-olive:#526044; --color-ink:#28221D;
  --color-background:var(--color-cream); --color-surface:#FFFFFF;
  --color-heading:var(--color-chocolate); --color-text:var(--color-ink);
  --color-muted:#6E6258; --color-border:#E4D7C1;
  --color-primary:var(--color-chocolate); --color-primary-hover:var(--color-cocoa);
  --color-accent:var(--color-gold);
  --font-heading:"Playfair Display",Georgia,serif; --font-body:"Inter",Arial,sans-serif;
  --container-width:1200px; --page-padding:24px; --section-space:88px;
  --radius-sm:6px; --radius-md:12px; --radius-lg:18px;
  --shadow-card:0 6px 24px rgba(53,23,15,0.08); --transition:220ms ease;
}

COLOR USAGE: ~60% cream/ivory (backgrounds, whitespace, cards), ~30% chocolate/cocoa (text, nav, buttons, footer), ~10% gold (borders, small icons, dividers, selected states). Never use gold for body text. Dark chocolate text on cream; cream text on chocolate. Verify WCAG AA contrast on all interactive elements.

TYPOGRAPHY AND UI RULES
- Headings: Playfair Display, medium weight, generous line height. Body/UI: Inter, 15–17px desktop.
- Buttons: sans-serif, medium weight, sentence case, radius 8–14px, smooth hover transition (primary → cocoa).
- Container max 1200px; desktop page padding 48–64px, mobile 18–22px; section spacing 72–100px desktop, 44–60px mobile.
- Borders 1px solid #E4D7C1; shadows only soft warm brown (--shadow-card), never black.
- Animations: subtle fade-in on scroll (IntersectionObserver), image zoom on card hover, smooth button transitions. Respect prefers-reduced-motion.

PRODUCT DATA (use exactly; do not invent products, prices or categories)
Categories: Varkey, Biscuits, Combos.
Items sold by weight, with price per size:
- Special Varkey: 250g ₹90 | 500g ₹160 | 1kg ₹280
- Regular Varkey: 250g ₹70 | 500g ₹140 | 1kg ₹260
- Crispy Varkey: 250g ₹80 | 500g ₹150 | 1kg ₹280
- Mini Varkey: 250g ₹100 | 500g ₹180 | 1kg ₹300
- Varkey Flakes: 250g ₹50 | 500g ₹90 | 1kg ₹150
- Salt Biscuit: 250g ₹90 | 500g ₹160 | 1kg ₹280
- Sweet Biscuit: 250g ₹90 | 500g ₹160 | 1kg ₹280
Combos (1 kg total, fixed price):
- Bestseller Combo ₹290: Special Varkey 500g + Regular Varkey 500g
- Ooty Signature Combo ₹300: Special Varkey 250g + Crispy Varkey 250g + Regular Varkey 250g + Salt Biscuit 250g
- Tea Time Combo ₹300: Special Varkey 250g + Sweet Biscuit 250g + Salt Biscuit 250g + Varkey Flakes 250g
Store in data/products.json and data/combos.json (fields: id, name, category, description placeholder, image path, sizes[{label, grams, price}] or price + includes[]). Use image placeholders with proper alt text and a graceful fallback if an image is missing. Leave description, ingredients and allergens as clearly marked "TODO: confirm with bakery" placeholders; never fabricate them.

PAGE REQUIREMENTS

1) HOME (/)
Announcement bar (editable text) → sticky header (logo, Home, Shop, About, Blog, search icon, cart icon with live count badge) → hero (large image, headline "Every Bite Tells a Story.", supporting text "Discover the warmth of freshly baked favourites, made for life's sweetest moments.", CTA "Shop now") → featured categories (Varkey, Biscuits, Combos) → bestsellers (render the 3 combos plus top items as cards from JSON, with size selector and quick-add) → Our Story teaser with link to About → "Freshly baked" craftsmanship section → testimonials (use a clearly marked placeholder block; real reviews only, do not invent) → newsletter signup (front-end validation only, with a TODO for connecting a real email service) → footer.

2) SHOP (/shop.html)
Heading "Made Fresh, Shared with Love." Category filter chips (All, Varkey, Biscuits, Combos), client-side search, sorting (featured, price low→high, price high→low, name A–Z), responsive product grid (4 columns large desktop, 3 desktop, 2 mobile). Each card: image, name, size/weight selector that updates the displayed price live, Add to cart. Product detail modal or drawer: larger image, description, what's included (for combos), availability, quantity stepper. Empty-state message when no products match. Cart drawer: quantity +/- controls, remove, per-line price, subtotal, "Order on WhatsApp" button that opens https://wa.me/<PHONE_PLACEHOLDER>?text=<URL-encoded order summary listing items, sizes, quantities, total>. Keep the WhatsApp number in one config constant at the top of cart.js. State: JS + localStorage (wrapped in try/catch), persists across pages. No fake payment or checkout.

3) ABOUT (/about.html)
Hero "A Tradition Baked into Every Bite." Sections: brand story, journey timeline, craftsmanship, people behind the bakery, values (freshness, consistency, quality, customer care), visit us (address, map embed placeholder, opening hours, phone), CTA "Explore our shop". Use clearly marked TODO placeholders for history, dates, awards and team; DO NOT invent establishment dates, awards or ingredient claims.

4) BLOG (/blog.html)
Hero "Stories from Our Oven." Featured article, article grid with categories (Baking Tips, Bakery Stories, Ingredients, Recipes, News), keyword search and category filter. Article detail rendered from blog.html?slug=... using data/posts.json: title, cover image, author, date, reading time, content, related posts, copy-link and social share buttons. Seed with 3 short placeholder posts marked as sample content. SEO: unique <title>, meta description, canonical URL, and Article JSON-LD generated for the detail view.

GLOBAL REQUIREMENTS
- Mobile-first responsive design with CSS media queries (breakpoints ~480, 768, 1024, 1280) in responsive.css; accessible hamburger menu in JS (aria-expanded, Esc to close, focus trap).
- Semantic HTML (header, nav, main, section, article, footer), one h1 per page, alt text on all images, visible focus outlines, full keyboard navigation, aria-live for cart updates, skip-to-content link.
- Performance: loading="lazy" on below-fold images, width/height attributes to prevent layout shift, WebP images, no unused CSS/JS.
- SEO: unique title and meta description per page, Open Graph tags, sitemap.xml and robots.txt.
- Footer: contact details, opening hours, social links, policies (placeholders), copyright.
- Security: never include secret API keys in frontend code; sanitize/escape any text inserted via innerHTML (prefer textContent).
- Code quality: modular, commented, consistent naming (BEM-style classes), no inline styles, no duplicated CSS, no console errors.

DELIVERABLES
1. Every file in the folder structure with full, working code (no "rest of code here" omissions).
2. master_notes.md documenting design tokens, how to add products or posts, where to set the WhatsApp number, and a TODO checklist of real content the owner must supply (photos, history, address, hours, reviews, allergens).
3. A short README section on running locally with a simple static server.

Build file by file in this order: variables.css → style.css → responsive.css → header.html/footer.html → main.js → JSON data → index → shop (+cart.js, products.js) → about → blog (+blog.js) → sitemap/robots → master_notes.md. After finishing, self-review against the checklist above and list any assumptions made.

---

# BUILD DOCUMENTATION (delivered with the site)

## 1. Design tokens

All tokens live in `css/variables.css` inside `:root`. **Never hard-code colors
elsewhere** — always use the variables.

| Token | Value | Use for |
|---|---|---|
| `--color-chocolate` | `#35170F` | Primary text, nav, buttons, footer bg |
| `--color-cocoa` | `#6B3821` | Button hover, secondary emphasis |
| `--color-gold` | `#C79A42` | Accents only: dividers, rules, focus rings, borders, icons, selected states. Never body text |
| `--color-ivory` | `#F2E4C5` | Hero/page-hero backgrounds, subtle fills |
| `--color-cream` | `#FBF7EF` | Page background, button text on dark |
| `--color-wheat` | `#D8C7A4` | Footer text |
| `--color-cinnamon` | `#75432D` | Rare warm accents |
| `--color-olive` | `#526044` | WhatsApp order button |
| `--color-ink` | `#28221D` | Body text |
| `--color-border` | `#E4D7C1` | All 1px borders |
| `--font-heading` | Playfair Display | All headings |
| `--font-body` | Inter | Body and all UI/buttons |
| `--container-width` | `1200px` | Max content width |
| `--shadow-card` | warm brown shadow | Cards only — never black shadows |
| `--transition` | `220ms ease` | All hover/state transitions |

Color balance: ~60% cream/ivory, ~30% chocolate/cocoa, ~10% gold.

## 2. How to add a product

1. Open `data/products.json` and add an object to the `products` array:

```json
{
  "id": "my-new-varkey",
  "name": "My New Varkey",
  "category": "Varkey",
  "description": "TODO: confirm with bakery",
  "ingredients": "TODO: confirm with bakery",
  "allergens": "TODO: confirm with bakery",
  "image": "assets/images/products/my-new-varkey.webp",
  "featured": false,
  "sizes": [
    { "label": "250g", "grams": 250, "price": 90 },
    { "label": "500g", "grams": 500, "price": 160 },
    { "label": "1kg", "grams": 1000, "price": 280 }
  ]
}
```

2. Drop the photo (WebP, ~800×600) at the given `image` path. If the file is
   missing, the card shows a graceful "photo coming soon" fallback — the page
   never breaks.
3. Set `"featured": true` to show it among the home-page bestsellers.
4. Valid `category` values: `Varkey`, `Biscuits`.

## 3. How to add a combo

Open `data/combos.json`:

```json
{
  "id": "my-combo",
  "name": "My Combo",
  "category": "Combos",
  "description": "TODO: confirm with bakery",
  "image": "assets/images/products/my-combo.webp",
  "weight": "1 kg total",
  "price": 300,
  "featured": true,
  "includes": [
    { "productId": "special-varkey", "name": "Special Varkey", "quantity": "500g" },
    { "productId": "salt-biscuit", "name": "Salt Biscuit", "quantity": "500g" }
  ]
}
```

Combos have a fixed `price` and no `sizes` — the UI adapts automatically.

## 4. How to add a blog post

Open `data/posts.json` and add to the `posts` array:

```json
{
  "slug": "my-post-slug",
  "title": "My Post Title",
  "category": "Recipes",
  "author": "Author name",
  "date": "2026-02-01",
  "readingTime": "4 min read",
  "featured": false,
  "image": "assets/images/blog/my-post.webp",
  "excerpt": "Short summary shown on the list page.",
  "content": [
    { "type": "p", "text": "A paragraph." },
    { "type": "h2", "text": "A section heading" },
    { "type": "list", "items": ["Bullet one", "Bullet two"] },
    { "type": "ol", "items": ["Step one", "Step two"] }
  ]
}
```

- Post URL: `blog.html?slug=my-post-slug`
- Valid `category`: `Baking Tips`, `Bakery Stories`, `Ingredients`, `Recipes`, `News`
- `"featured": true` pins it as the featured article on the blog list.
- Title, meta description, canonical, Open Graph tags and Article JSON-LD are
  generated automatically for the detail view.

## 5. Where to set the WhatsApp number

Top of `js/cart.js`:

```js
const WHATSAPP_NUMBER = "919344921647"; // +91 93449 21647 (owner-confirmed)
```

Use country code + digits only. This is the single config point — every
"Order on WhatsApp" click builds `https://wa.me/<number>?text=<URL-encoded
order summary>` from it. The same number appears in `footer.html` (tel +
WhatsApp links) and `about.html` (Phone &amp; WhatsApp card).

## 6. Other things to configure

- **Domain**: replace `https://www.vasuettanbakery.com` in `sitemap.xml`,
  `robots.txt`, `SITE_URL` (top of `js/blog.js`) and canonical/OG tags in the
  four HTML pages.
- **Announcement bar**: currently commented out in `header.html` — uncomment to re-enable.
- **Address / hours / phone**: `footer.html` and the Visit Us section in `about.html`
  (Kotagiri + phone +91 93449 21647 confirmed; street address and hours still TODO).
- **Social & maps links**: Instagram + Google Maps URLs are in `footer.html` and
  the map card in `about.html`.

## 7. TODO checklist — real content the owner must supply

- [ ] Bakery logo (`assets/images/logo.png`) and hero photo (`assets/images/hero-bakery.webp`)
- [ ] Product photos for all 7 products + 3 combos (`assets/images/products/*.webp`)
- [ ] About-page photos (`assets/images/about/`) and blog cover images (`assets/images/blog/`)
- [ ] Real product descriptions, ingredients and allergen info (replace every
      "TODO: confirm with bakery")
- [x] Founding year (Since 1980, owner-confirmed) — later timeline milestones
      and any awards still need verified dates
- [ ] Team names, roles and photos
- [ ] Exact street address and opening hours (location and phone confirmed)
- [x] Phone / WhatsApp number: +91 93449 21647 (footer, About, cart config)
- [ ] Verified customer reviews (replace the three placeholder testimonials —
      do not publish invented reviews)
- [ ] Google Maps embed code for the Visit Us placeholder
- [x] Instagram profile (added to footer) and Google Maps link (About page + footer)
- [ ] Real domain for sitemap/robots/canonical/OG tags
- [ ] Email newsletter provider (form validates only; nothing is sent yet)
- [ ] Privacy policy / terms / shipping pages
- [ ] Favicon

## 8. Running locally

See `README.md` — use VS Code **Live Server** (or `python -m http.server 8080`).
Opening pages via `file://` shows a fallback note instead of the header/footer
because `fetch()` is blocked on that protocol.

## 9. Assumptions made

1. **Domain**: `www.vasuettanbakery.com` used as a placeholder everywhere.
2. **Location & contact**: Kotagiri, The Nilgiris, phone/WhatsApp +91 93449 21647
   and "Since 1980" are owner-confirmed; full street address and opening hours
   remain TODO. Instagram profile and Google Maps link are owner-supplied and live.
3. **Prices/weights**: taken exactly from the brief; nothing invented.
4. **Descriptions/ingredients/allergens**: left as "TODO: confirm with bakery".
5. **Blog posts**: 3 short samples explicitly marked "SAMPLE CONTENT".
6. **Testimonials and team**: placeholder blocks, explicitly not real reviews.
7. **Bestsellers on home**: 3 combos + the 3 products flagged `featured`
   (Special Varkey, Regular Varkey, Salt Biscuit).
8. **Cart behaviour**: quantity ≤ 20 per line; cart persists via localStorage
   (try/catch for private-mode browsers); no payment/checkout — WhatsApp only.
9. **No image assets were created** (binary files); every image slot has a
   graceful fallback until real photos are added.

### Premium design pass (v2)

The site now ships a richer heritage styling built from the same palette:

- Ornamental gold rules and diamond dividers under section headings
- Kicker labels flanked by gold hairlines (cocoa text for AA contrast)
- Gradient chocolate buttons with gold inset hairline; gold CTA on the dark hero
- Dark gradient category cards with gold inner frame and orbit detail
- Product/post cards get a gold top rule on hover and serif price treatment
- Ivory page heroes with subtle diagonal wheat texture and gold edge bars
- Glassy sticky header, gold underline nav indicators, gradient cart badge
- Testimonials with oversized gold quote marks; value cards with gold crown
- Newsletter panel framed in gold with corner orbits; footer with gold gradient top strip
- All new shadows/hairlines/texture values are tokens in css/variables.css
  (nothing hard-coded in style.css)

### Live links supplied by the owner (added)

- Instagram: https://www.instagram.com/vasu_ettan_bakery_cakes?vrfl=c3kzeDdqbTI0djA3 (footer social icon)
- Google Maps: https://maps.app.goo.gl/34eZL2XermHqfsZL7 (About page map card + footer)
- Brand greeting (footer, About hero/story, home story teaser): "Warm greetings from Vasu Ettan Bakery, Kotagiri! We are proud manufacturers of Ooty Varkey with 45+ years of baking tradition..."
- Phone / WhatsApp: +91 93449 21647 (footer tel + wa.me links, About card, js/cart.js)
- Owner copy added: "Authentic Ooty Varkey", "Since 1980", "Retail & Wholesale Varkey & Biscuits", "Pre-Order Cakes also Available" (hero eyebrow, About, shop, footer, home teaser)
