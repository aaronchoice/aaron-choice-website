# Aaron Choice — Website

A static site for Aaron Choice (premium botanical supplements): a marketing homepage (`index.html`), a full retail Shop page (`shop.html`), and a research Blog (`blog.html`). Pure HTML/CSS/JS, no build step, no dependencies.

## Deploying to Cloudflare Pages (via GitHub)

1. **Push this folder to a GitHub repo.**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Aaron Choice site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

2. **Connect the repo to Cloudflare Pages.**
   - Go to the [Cloudflare dashboard](https://dash.cloudflare.com/) → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**.
   - Select this repository and authorize access.

3. **Build settings.**
   - Framework preset: **None**
   - Build command: *(leave blank)*
   - Build output directory: `/` (root)
   - No environment variables are needed.

4. **Deploy.**
   - Click **Save and Deploy**. Cloudflare will serve `index.html` at the root of your `*.pages.dev` URL within a minute or two.
   - Every future push to `main` auto-deploys.

5. **Custom domain (optional).**
   - In the Pages project → **Custom domains** → add your domain and follow the DNS instructions (Cloudflare will auto-configure this if the domain is already on Cloudflare).

## QA pass (2026-09-17)

Fixed:
- All emoji (trust bar, ingredient icons, hamburger, search, close button) replaced with custom line-style SVG icons matching the navy/gold palette
- Trust bar redesigned — icon badges, dividers, tighter type for a more premium feel
- Mobile menu is now functional (slide-out panel with nav links) instead of an alert
- Search icon opens a real inline filter — typing a product name dims non-matching cards and scrolls to the shop section (still a lightweight client-side filter, not a full search backend)
- Cart now tracks quantity per product (adding the same item twice increments qty instead of creating duplicate rows), with +/− controls
- Star ratings have hidden text for screen readers ("Rated 5 out of 5 stars")
- Price formatting made consistent ($27 across all products, was a mix of "$27.00" and "From $27")
- Added favicon, Open Graph/Twitter meta tags, `robots.txt`, `sitemap.xml`, and a Cloudflare `_headers` file with baseline security headers
- Removed dead JS (an empty event listener)
- Product images lazy-load below the fold

## Product photography & Blog (2026-09-17)

- Replaced the Moringa product image with the real Aaron Choice product photo, and added **Hummingbird Flower Powder Capsules** ($35) as a fifth product with its own photo. Both images live in `images/` (resized/compressed for web) instead of hotlinking.
- Added a **"The origin of disease"** section below the hero with a supplied infographic — flagged in-page with a disclaimer, since content connecting a supplement brand to "causes of disease" is the most disease-adjacent material on the site and should get a compliance review before launch (FTC/FDA rules on implied disease claims for supplements are strict).
- Added **`blog.html`** — a Blog page, linked from the main nav/footer/mobile menu, organized by ingredient (Black Turmeric, Ashwagandha, Jackfruit, Amla, Moringa, Hummingbird Tree Flower) with jump-to-section pills. It compiles:
  - The original featured Semantic Scholar citation (Black Turmeric / ABTS antioxidant study), and
  - 26 additional PubMed/PMC citations supplied via `Aaron_Choice_Scientific_Publication_Links.docx`, grouped under their ingredient.
  - **Titles shown in italics** on a handful of entries are topic descriptors (as given in the source document), not confirmed published titles — PubMed blocks automated fetches with a bot-check, so those specific titles couldn't be independently verified. Everything else shown in normal type was confirmed against a live search of the PMID. Recommend spot-checking the italicized ones before this page is considered final.
  - A disclaimer at the bottom clarifies these citations are educational context, not medical advice or disease claims about the products.

## Shop page & origin section redesign (2026-09-17)

- **Built `shop.html`** — a dedicated retail page for the full product catalogue, linked from the nav, hero, mobile menu, footer and homepage product teaser (which now says "View the full shop →"). It includes:
  - Filter pills by wellness goal (Joint & Mobility, Digestive Wellness, Antioxidant Support, Daily Wellness), matching the categories used in the homepage Product Finder.
  - A sort dropdown (Featured / Price: Low–High / Price: High–Low / Name A–Z) with a live "N products" count.
  - All 5 products (Black Turmeric, Cinnamon, Jackfruit, Moringa, Hummingbird Flower Powder), each with a quantity stepper and its own "Add to Cart" button.
  - The same cart drawer, toast notifications, mobile menu and footer as the rest of the site, so it feels like one continuous store rather than a bolted-on page.
  - Tested end-to-end (filtering, sorting, quantity stepper, add-to-cart, cart drawer, mobile layout) — all working with no JS errors.
- **Redesigned "The origin of disease" section** on the homepage: it was too visually heavy as a single large centered image. It's now a compact two-column layout — copy on the left, image on the right — and the image opens in a full-screen lightbox on click for closer viewing. The compliance disclaimer under the image is unchanged.

## Logo, favicon, search & alignment fixes (2026-09-17)

- **Real logo added**: the circular "Community Health & Prevention Care Inc. / Aaron Choice" emblem now appears next to the wordmark in the nav on every page (`images/aaron-choice-logo.png`, background removed). The favicon and Apple touch icon (`images/favicon.png`, `images/apple-touch-icon.png`) use the simplified two-hands mark on its own — it reads more clearly than the full text badge at browser-tab size.
- **Logo made bigger, hung as a tag from the header**: the badge is now much larger and its flat top edge sits flush against the line between the announcement bar and the nav, so it reads as a tag or medallion hanging down from that line rather than a small icon sitting inline with the text. The "Aaron Choice" wordmark next to it now uses **Luckiest Guy** (Google Font) to match the lettering style used inside the logo itself, in the same dark navy as the rest of the site. Note: this sandbox blocks Google Fonts, so I couldn't preview the exact rendering myself — it'll load correctly once the site is live, since it uses the same Google Fonts mechanism as the existing Playfair Display / DM Sans fonts already on the site.
- **Shop page card alignment**: quantity stepper and "Add to Cart" button now line up on the same row across all product cards, regardless of how long a product's description or tag list runs (previously Black Turmeric's extra tag caused its row to sit lower than the others).
- **Homepage search fixed**: typing in the nav search now filters live (as you type) instead of only on Enter, and there's a visible "Clear search" link plus an × button in the search box — previously, clearing the box didn't restore the other products without pressing Enter again, which could leave them stuck dimmed.

## Lifestyle images as primary photos & card alignment (2026-09-17)

- **Lifestyle images now lead everywhere**: the homepage teaser grid and the Shop page catalogue both show each product's Lifestyle (in-context) photo as the main card image instead of the Studio cutout. The Shop page's lightbox carousel still includes both — it now opens on the Lifestyle image first, with the Studio cutout as the second slide, matching what's shown on the card.
- **Homepage price/Quick Add row alignment fixed**: product cards are now equal-height flex columns, so the price and "Quick Add" button always sit on the same row across all cards regardless of how long a description runs (the Shop page already had this fix from an earlier round).
- Card images switched from `object-fit:contain` (sized for isolated cutouts) to `object-fit:cover` (full-bleed) on the homepage, since Lifestyle photos are in-context shots rather than transparent cutouts.

## Hero redesign & two new products (2026-09-17)

- **Homepage hero redesigned**: replaced the simple centered-icon hero with a full-bleed lifestyle photo (Black Turmeric bottle among fresh turmeric root and leaves), a soft bottom gradient for text legibility, an italic serif "Wellness Inspired By Nature" watermark, and a caption naming the flagship botanical. The copy side now includes three badge callouts (Pure Ingredients, Real Wellness, A Brighter Tomorrow) beneath the CTA buttons, matching the richer reference layout you shared.
- **Two new products added** — Ashwagandha & Amla Extract Capsules ($29) and Cinnamon Oil ($19) — to both the homepage teaser grid and the full Shop page, each tagged "New." Both include Studio (background-removed) and Lifestyle images and are wired into the Shop page's lightbox carousel, filters (Daily Wellness / Antioxidant Support), sorting, and cart exactly like the original five products.
  - The two new source images you sent had a checkerboard "transparency" pattern baked into flat pixels rather than a real alpha channel, so I rebuilt clean transparent cutouts from them programmatically (edge-aware background detection, not a simple color key) before optimizing them the same way as the rest of the catalogue.
  - **Prices are placeholders** — set to fit the existing $19–$35 range. Update `data-price` and the visible `$` amounts in `shop.html` (and the matching `addCart(...)` price in `index.html`) once you have real pricing.
- Fixed a small stale bug from the previous round: the Shop page's "N products" counter now always reflects the true count on page load (it previously showed a hardcoded "5 products" until you touched a filter).

## New product photography & lightbox carousel (2026-09-17)

- **All 5 products now use your own photography** — no more Wix hotlinks anywhere on the site. For each product you supplied two shots: a lifestyle photo (with background) and a studio cutout (transparent background). Both are hosted locally in `images/`:
  - Studio cutouts (`*-studio.webp`) are used for the catalogue grid on `shop.html` and the homepage teaser/hero on `index.html` — transparent background keeps them looking consistent against the site's colors.
  - Lifestyle photos (`*-lifestyle.jpg`) are used as the second image in each product's lightbox.
- **Shop page product lightbox**: clicking any product image on `shop.html` now opens a full-screen lightbox carousel showing that product's Studio and Lifestyle images, with:
  - Crossfade transition between images
  - Dot indicators and prev/next arrow buttons
  - Keyboard support (← → to switch images, Esc to close)
  - Click-outside-to-close
- Tested across all 5 products — both images load correctly in every case, and existing filtering/sorting/cart functionality has no regressions.

### Separate product pages vs. the lightbox carousel — my recommendation

You asked whether each product should get its own dedicated page instead. For a 5-product catalogue like this, **the lightbox carousel is the right call for now** — it's fast to browse, keeps people on the Shop page (so filtering/sorting/cart stay one click away), and it's what you already have live. Full product detail pages are the more "regular retail" pattern, but they earn their keep when there's more to say per product: longer descriptions, ingredient/dosage breakdowns, individual customer reviews, FAQs, or SEO copy you want Google to index under its own URL. Right now every product's info fits in the card itself, so a separate page would mostly just repeat what's already on `shop.html` with extra clicks in between.

My suggestion: keep the lightbox for now, and revisit dedicated pages once (a) the catalogue grows past ~10–15 SKUs, or (b) you have enough unique content per product (lab results, usage guides, verified reviews) to justify a page each. If you want, I can build out one example product page later so you can compare the experience directly before deciding.

## Full-bleed hero & Origin of Disease redesign (2026-09-17)

- **Hero section is now truly full-bleed**: the image is a single absolutely-positioned background layer (`.hero-bg`) that covers the entire hero section — the full width and height of the browser window, not just a column beside the text. The heading, copy and buttons sit directly on top of the photo, in white, with a dark gradient scrim (darkest on the left, fading out toward the right) so the text stays readable against a busy photo. This holds at every width — desktop, tablet and mobile all show the photo as the full hero background, just with the scrim tuned per breakpoint (a left-to-right fade on wide screens, a flatter overall darkening on narrow ones where the text spans the full width). Verified at 1920px, 1440px, tablet (768px) and mobile (390px).
- **"The origin of disease" section redesigned** to match a richer reference layout:
  - The wheel infographic now sits inside a padded cream circle (pure CSS — no new image needed) with a soft shadow, and a "Click to enlarge" hint on hover.
  - Two decorative leaf-branch images (`images/leaf-branch-1.png`, `images/leaf-branch-2.png`) frame the circle at the top-left and bottom-left corners.
  - Added a faint decorative ring behind the section, vertical "Science / Nature / People" text, a rotated "A Healthier Tomorrow" accent, and a single-row of three icon callouts (Genetics, Lifestyle, Environment) reusing the site's existing icon style — no new icon images were needed.
  - The compliance disclaimer beneath the image is unchanged.
- Both sections were rebuilt in `index.html` only; `shop.html` and `blog.html` are untouched and were re-tested to confirm no regressions (product filters, cart, lightbox carousel, and page load all still work with no console/page errors — aside from a Google Fonts request, which is blocked only in this sandbox and will load normally once the site is live).
- **Still pending, awaiting more of your redesigned images**: Footer, the secondary "Start your wellness journey" hero (sits just above the footer), FAQ, testimonials, ingredient cards, and the science-process/benefits icon rows. The homepage product/collection grid is intentionally unchanged, per your note that it already looks right.

## Notes / things to swap before going live

- **Checkout**: the "Proceed to Checkout" button still shows an alert. Wire this to a real cart/checkout provider (Shopify, Stripe Checkout, Snipcart, etc.) before launch.
- **Search**: currently a simple client-side name filter over the products shown. If your catalogue grows or you want full-text/typo-tolerant search, connect a real search service.
- **Reviews**: sample testimonials are included; replace with verified customer reviews before launch (using placeholder names/quotes as if genuine is a legal risk once live).
- **Legal/compliance copy**: the FAQ and footer include notes flagging language that should be reviewed against your actual return policy, supplement regulations, and SKU-level claims before publishing.

## File structure

```
.
├── index.html    # the marketing homepage (HTML + CSS + JS inline)
├── shop.html     # the full retail Shop page (filter, sort, cart)
├── blog.html     # the research Blog, organized by ingredient
├── images/       # product photos and the "origin of disease" infographic
├── _headers      # Cloudflare Pages response headers
├── robots.txt
├── sitemap.xml
└── README.md     # this file
```
