# Aaron Choice — Website

A static site for Aaron Choice (premium botanical supplements): a marketing homepage (`index.html`), a full retail Shop page (`shop.html`), a research Blog (`blog.html`), and an About page (`about.html`). Pure HTML/CSS/JS, no build step, no dependencies.

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
  - Two decorative leaf-branch images (`images/leaf-branch-1.png`, `images/leaf-branch-2.png`) frame the circle at the top-left and bottom-right corners.
  - Added a faint decorative ring behind the section and a single-row of three icon callouts (Genetics, Lifestyle, Environment) reusing the site's existing icon style — no new icon images were needed.
  - The compliance disclaimer beneath the image is unchanged.
- **Origin of Disease follow-up fixes (2026-09-17)**: swapped in a freshly regenerated wheel infographic (`images/origin-of-disease.png`) that isn't cropped/cut off, and which already has its own padded circle and shadow baked in — the old CSS-drawn cream circle/padding/shadow wrapper was removed since it's no longer needed. The two leaf branches were repositioned to sit directly behind the circle's own edges (top-left and bottom-right) so they read as tucked behind the graphic rather than floating loose in the corners of the section. Removed the vertical "Science / Nature / People" text and the rotated "A Healthier Tomorrow" text per your feedback — the section is now just the circle, its two leaf accents, the caption, and the copy/icon column.
- **Origin of Disease rebuilt on your two regenerated images (2026-09-17)**: you supplied a full-section background photo (`images/origin-bg.jpg` — soft leaves and a faint decorative ring, matching the hero's full-bleed treatment) and a new wheel infographic that already has its leaf framing baked directly into the graphic (`images/origin-of-disease.png`, replacing the previous version). The section now uses the same full-bleed background pattern as the hero — the photo covers the entire section edge-to-edge — and the separate CSS-positioned leaf-branch images/logic from the last two rounds were removed entirely, since the leaves are now part of the supplied artwork itself. The "Click to enlarge" hint was moved to sit just below the wheel's outer ring so it doesn't overlap the diagram's labels. `images/leaf-branch-1.png` and `images/leaf-branch-2.png` are no longer referenced anywhere — safe to delete if you don't need them for anything else.
- Both sections were rebuilt in `index.html` only; `shop.html` and `blog.html` are untouched and were re-tested to confirm no regressions (product filters, cart, lightbox carousel, and page load all still work with no console/page errors — aside from a Google Fonts request, which is blocked only in this sandbox and will load normally once the site is live).
- **Still pending, awaiting more of your redesigned images**: Footer, the secondary "Start your wellness journey" hero (sits just above the footer), FAQ, testimonials, ingredient cards, and the science-process icon row. The homepage product/collection grid is intentionally unchanged, per your note that it already looks right.

## "Why Aaron Choice" section redesign (2026-09-17)

- Rebuilt the existing "Why Aaron Choice" section (previously plain navy background with a bare 4-column text grid) using your reference layout and new assets:
  - A full-bleed background photo (`images/benefits-bg.jpg`) — a leaf branch and forest bokeh — with a dark navy radial tint over most of the section so the white text stays readable, fading out toward the top-right corner so the leaf branch shows through clearly, matching your reference.
  - Added the subheading paragraph ("From nature to your wellbeing…") beneath the "The standard we hold ourselves to." headline, with a blue accent dot to match the rest of the site's headings.
  - Each of the 4 cards (Botanically Pure, Science Backed, Transparently Made, Quality Focused) now has its own circular icon image above the number — `images/benefit-botanically-pure.png`, `images/benefit-science-backed.png`, `images/benefit-transparently-made.png`, `images/benefit-quality-focused.png` (resized down from your originals since they were much larger than needed at this display size). Cards now have rounded corners and a subtle border/hover treatment on the semi-transparent glass background.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Icon size bump on "Why Aaron Choice" (2026-09-17)

- Increased the 4 benefit icons from 110px to 150px per your feedback — checked they still fit cleanly in the cards at desktop, tablet (2-column) and mobile widths.

## Science section redesign (2026-09-17)

- Rebuilt the "Our formulation approach" / "Know what you're taking" section (`#science`) using your reference layout and new assets:
  - A full-bleed dark background photo (`images/science-bg.jpg` — leaves and rock over a navy backdrop) with a flat dark overlay for text contrast, matching the hero/benefits full-bleed treatment.
  - The 5-step formulation flow (Botanical Source → Extraction → Formulation → Quality Testing → Finished Product) now has its own circular photo for each step (`images/science-01-source.png` through `images/science-05-finished.png`, resized down from your originals) next to the step number and heading, connected by a thin vertical line, with a "Pure Botanicals / Real Impact" label at the bottom.
  - The right column's 4 info cards (Ingredient transparency, Evidence-ready, Batch transparency, Responsible claims) each got a circular line-icon (leaf, document, flask, shield) matching the site's existing icon style — no new images needed there.
  - Added a "Plants · People · A Healthier Tomorrow" line in the bottom-right corner, matching your reference.
  - Fixed a CSS specificity bug while building this: the card border/background rule was initially matching every `<div>` inside the info cards (including the inner text wrapper), producing a "double card" look — scoped it to direct children only.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Ingredient intelligence section redesign (2026-09-17)

- Rebuilt the "Ingredient intelligence" section (`#ingredients`) — previously a plain 3-column bordered card grid with generic line-icons — using your reference layout and new assets:
  - A full-bleed light background photo (`images/ingredients-bg.jpg` — soft leaf branches and thin arc lines in each corner) behind the whole section, matching the airy look of the reference. No dark tint needed here since the section uses dark text on a light background.
  - Added the top-right "Plants with purpose." / "TRUSTED BY SCIENCE." decorative label (with a white text-glow so it stays legible over the leaf branch behind it), matching the reference.
  - Each of the 3 cards (Black Turmeric, Black Pepper Extract, Ginger Root) now has its own product photo — `images/ingredient-black-turmeric.png`, `images/ingredient-black-pepper.png`, `images/ingredient-ginger-root.png` (resized down from your originals) — bleeding past the right edge of the card, plus a numbered label (01/02/03), the green small-caps subtitle, and a "LEARN MORE →" link, matching the reference card layout.
  - Added the bottom-left "REAL INGREDIENTS · REAL EVIDENCE · REAL IMPACT" line, also with a white text-glow for legibility over the leaves.
  - On tablet/mobile, cards stack to a single column and the ingredient photos shrink so nothing overlaps the copy.
- Verified at desktop, tablet, and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Ingredient intelligence section polish (2026-09-17)

- Removed the "Real Ingredients · Real Evidence · Real Impact" line from the bottom of the section per your feedback.
- Gave the 3 ingredient cards a frosted/translucent glass look (semi-transparent white background with a backdrop blur, softened border and shadow) so the leaf background shows through them, with a slightly stronger glass effect on hover.
- Re-ran the full regression suite on shop.html and blog.html — no errors.

## Personalised Discovery (product finder) background (2026-09-17)

- Added a full-bleed background photo (`images/finder-bg.jpg` — a mortar and pestle with basil leaves on a dark navy backdrop, with the same thin arc-line accents as the ingredients background) to the "Personalised discovery" / "Find your Aaron Choice" section, replacing the flat navy gradient.
- Kept a dark gradient tint over the photo so the white heading/body text and the white finder card stay fully readable, matching the full-bleed treatment used on the hero, benefits and science sections.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Community (reviews) and FAQ backgrounds + frosted glass (2026-09-17)

- Added a full-bleed background photo (`images/community-bg.jpg` — soft leaf branches and shadow on a white wall) to the "Community" / "What customers say" reviews section, and a full-bleed background photo (`images/faq-bg.jpg` — a mortar and pestle with leaves on a marble table) to the "Frequently asked" FAQ section, both matching the airy full-bleed treatment used on the ingredients section.
- Introduced a shared `.glass-card` style (translucent white background with a backdrop blur, soft border and shadow, slightly stronger on hover) and applied it to the 3 review cards and to the FAQ panel, so the backgrounds show through consistently — the same frosted-glass look already used on the ingredient cards.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Secondary hero + footer redesign (2026-09-17)

- Added a full-bleed light background photo (`images/cta-bg.jpg` — the capsule bottle and mortar/pestle on a marble podium) to the "Start your wellness journey" section right above the footer, with a soft radial white vignette behind the centered text so it stays fully readable while the product shot shows through at the edges.
- Added a full-bleed dark background photo (`images/footer-bg.jpg` — leaf branches on a navy backdrop) to the footer, with a dark gradient tint for contrast.
- Rebuilt the footer to match your reference: a larger "Aaron Choice" logotype with a "PLANTS PEOPLE PURPOSE" tagline and circular social icons (Instagram, Facebook, YouTube, Pinterest, LinkedIn — currently placeholder `#` links); a "REAL INGREDIENTS / REAL IMPACT" label in the top-right corner; rounded out the Shop/Science/Support link columns to match your reference (added Gift Cards, Research & Evidence, Subscriptions, Terms of Service); a new "A Healthier Tomorrow" + "Stay in the know" newsletter signup row (submitting shows a confirmation toast — no email service is wired up yet); and a "🍁 Proudly Canadian" line next to the copyright.
- Fixed a pre-existing CSS bug found while doing this: the footer's link-list styling (`.footer h4/ul/li`) was targeting a `.footer` class that no elements actually had, so footer links were rendering with default browser bullets and unstyled headings — this was invisible before because it blended into the plain dark background, but shows up now. Corrected the selectors to target the `<footer>` element directly.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Trust bar restyle (2026-09-17)

- Restyled the trust bar between the nav and the hero (100% Plant-Based · Third-Party Tested · GMP Certified · Free Shipping · Secure Checkout) to match the rest of the homepage: it was using an orphaned gold/tan accent color (`--gold`) that wasn't used anywhere else on the site, small 14px icons, and small title-case text — swapped it to the same navy/blue palette and uppercase, letter-spaced label style used everywhere else (eyebrows, hero badges), with larger icon circles (38px) and bigger icons (19px).
- Redrew the "Third-Party Tested" icon (was an odd flask/hourglass shape) as a cleaner award-ribbon/seal icon, and refined the "Secure Checkout" lock and "Free Shipping" truck icons slightly.
- Bumped the label font size up (11px → 13px, and the tighter desktop-override size from 10px → 12.5px) so it reads more comfortably next to the rest of the page.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Origin of Disease section polish (2026-09-17)

- Made the "Root-Cause Thinking" eyebrow stand out: bumped it up to 13px, bolder weight, wider letter-spacing, a saturated blue instead of the pale blue that was blending into the light background, and added a short accent line in front of it.
- Turned the "For educational context only — not a diagnostic tool..." line under the wheel infographic into a proper callout: larger, bolder text in a bordered card with a blue accent stripe on the left, instead of small muted gray text that was easy to miss.
- Replaced the Genetics/Lifestyle/Environment icons with more purpose-built ones (a DNA double-helix for Genetics, a heart with a pulse line for Lifestyle, a globe with latitude lines for Environment) instead of a generic leaf and plain heart, increased their size, and switched them from a 3-across row (which was wrapping awkwardly with a stray divider line) to a cleaner stacked list with bigger label and description text.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Science section evidence cards polish (2026-09-17)

- Made the 4 evidence cards (Ingredient transparency, Evidence-ready, Batch transparency, Responsible claims) noticeably bigger — more padding, taller minimum height, larger icon circles (36px → 48px) — and increased the heading and description text size so they're easier to read at a glance.
- Replaced the icons with ones that match each card's meaning more clearly: a labeled clipboard for Ingredient transparency, an open book for Evidence-ready, a document with a lookup/magnifying glass for Batch transparency (Responsible claims keeps its shield-check).
- Removed the "Plants · People · A Healthier Tomorrow" line under the evidence cards per your feedback.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## Community/FAQ/CTA cleanup + eyebrow consistency (2026-09-17)

- **Community section**: removed the placeholder paragraph ("Review content should be populated from verified customer data in production...") next to the "What customers say" heading.
- **FAQ section**: shifted the FAQ panel (and heading) to the right side of the section so the mortar-and-pestle photo in the background is fully visible on the left, instead of being covered by the panel.
- **Secondary hero above the footer**: left-aligned the eyebrow/heading/paragraph/button (previously centered) and adjusted the background tint to a left-to-right fade, so the capsule bottle and mortar/pestle on the right are clearly visible instead of being partly washed out behind centered text.
- **Eyebrow consistency site-wide**: every small uppercase kicker label (Botanicals · Science · Transparency, Why Aaron Choice, Root-Cause Thinking, Science without the noise, Personalised discovery, What's Inside, Community, Support) now shares the same font size (13px), weight, letter-spacing and short accent-line treatment. Previously a leftover "premium" theme rule was silently shrinking every eyebrow down to 9px, and several of them (Community, Support, Personalised discovery, Aaron Choice on the CTA) used a pale light-blue that had very low contrast against light backgrounds — those now use a bold, readable blue, while eyebrows on dark photo backgrounds (hero, benefits, science, finder) keep a light blue for contrast there.
- Verified at desktop and mobile widths, and re-ran the full regression suite on shop.html and blog.html — no errors.

## New About page — Dr. Balasingham Arasabalan (2026-09-17)

- **Added `about.html`**, a new page profiling Dr. Balasingham Arasabalan (clinical psychology / social work / research), and added an **"About"** link as the first item in the main nav — before "Shop" — on every page (`index.html`, `shop.html`, `blog.html`, `about.html`), desktop and mobile menus alike.
- Content was sourced from the supplied document (`Dr_Balasingham_Arasabalan_Portfolio_About.docx`) and organized into sections that mirror the reference design you shared:
  - **Hero**: headline, intro paragraph, Toronto location, and two CTA buttons ("View Research", "Professional Profile").
  - **About intro**: a 3-column layout pairing a short bio with a decorative leaf image and a stacked list of his areas (Psychology, Mental Health, Behaviour, Physiology, Research).
  - **Clinical & Professional Practice**: a dark 3-item icon grid (Mental Health & Clinical Psychology, Psychological Assessment, Social Work).
  - **Featured Research**: a research card summarizing his published study, with real links to the publication and its DOI, alongside a diagram of his biofeedback → physiological regulation → metabolic measures research model.
  - **Research Interests**: a dark 6-item grid (Clinical Psychology, Psychophysiology, Heart-Rate Variability, Biofeedback, Mind–Body Health, Metabolic Health).
  - **"One system. Many perspectives."**: a CSS-only 5-circle Venn-style diagram (no image asset needed) showing how his focus areas overlap, next to a list of his professional focus areas.
  - A pull-quote/philosophy band, and a closing publication + "get in touch" call-to-action split section.
- **No real photo of Dr. Balasingham was supplied**, so the hero and the research card both use a placeholder treatment (soft gradient box, a line-style icon, and a small "coming soon" / "placeholder" label) instead of leaving a broken image or a stock photo standing in for him. Swap these for real photography/imagery whenever it's available — they're the `.about-photo` block in the hero and the `.research-visual` block in the Featured Research card.
- The page reuses the site's existing design tokens (navy/blue palette, Playfair Display + DM Sans, the same `.eyebrow` kicker style) so it reads as part of the same site rather than a bolted-on page, and reuses one existing image (`images/leaf-branch-1.png`) rather than adding new assets.
- Verified at desktop and mobile widths (including the new nav item doesn't cause any wrapping/overflow with all 8 nav links present), tested the mobile hamburger menu on the new page, and re-ran the full regression suite on `shop.html` and `blog.html` after the nav markup changed — no errors.

## Shop trust bar restyle + footer consistency (2026-09-17)

- **Shop page trust bar**: the "100% Plant-Based / Third-Party Tested / Secure Checkout / Free Shipping" strip previously sat at the very bottom of `shop.html`, right above the footer, using an older, smaller icon style with a gold accent color. It's now positioned right below the nav — in the same spot as the homepage's trust bar, right above the page content — and uses the exact same restyled look as the homepage (navy/blue palette, larger 38px icon circles, uppercase letter-spaced labels), including the "GMP Certified" item so it now matches the homepage's 5-item set exactly.
- **Footer made consistent across every page**: `index.html` had the fully redesigned footer (logo + tagline, social icons, 5 link columns, "Real Ingredients / Real Impact" corner label, "A Healthier Tomorrow" newsletter signup, "Proudly Canadian" line) from an earlier round, but `shop.html`, `blog.html` and `about.html` were still on an older, plainer footer with fewer links and no newsletter/social/tagline elements. All three now use the identical footer markup, styling and behavior as the homepage — same background photo treatment, same columns and links (adjusted so Science/Reviews/FAQ links point back to `index.html#section` from pages other than the homepage), and the same "Subscribed!" toast confirmation on the newsletter form (added the toast element and its script function to `blog.html` and `about.html`, which didn't have one yet).
- Also fixed a leftover instance of the pre-existing footer CSS bug (link/heading styles targeting a `.footer` class that no element actually has, which silently fell back to unstyled bullet links) that was still present in `shop.html`, `blog.html` and `about.html`'s old footer CSS — all three now use the corrected element-tag selectors.
- Linked "Our Story" (Company column) to `about.html` on every page, including the homepage, so it's consistent everywhere.
- Verified at desktop and mobile widths, confirmed the newsletter toast fires correctly on all four pages, and re-ran the full regression suite on `shop.html` and `blog.html` — no errors.

## Blog page redesign (2026-09-17)

- **Rebuilt `blog.html`** end-to-end to match your reference layout:
  - A new two-column hero ("The Science Behind Botanicals.") with intro copy, a "Real Ingredients. Real Research. A Healthier Tomorrow." tagline, and a full-bleed leafy image on the right with an italic "Nature backed by science." caption — reusing the existing `images/ingredients-bg.jpg` (no new asset needed).
  - A filter row: pill buttons for "All" and each of the 6 ingredients (now functional — click one to show only that ingredient's section) plus a live search box that filters articles by title across every group and shows a "No articles match your search" message when nothing matches.
  - Each ingredient is now a "Botanical Spotlight" row: a large image panel with the ingredient name/latin name on the left, and its 3 most relevant articles on the right (thumbnail, title, source/PMID, "Read →" link). Groups with more than 3 citations (Ashwagandha, Jackfruit, Amla, Moringa) get a "View all" link that expands the rest in place — nothing was removed, it's just collapsed by default the way your reference shows 3 per ingredient.
  - Black Turmeric's detailed featured-research summary (with the "Read on Semantic Scholar" link) is preserved as a highlighted block above its article list.
  - **Images reused, no new assets needed**: the spotlight panels use your existing product lifestyle photos — `black-turmeric-lifestyle.jpg`, `jackfruit-lifestyle.jpg`, `moringa-lifestyle.jpg`, `hummingbird-lifestyle.jpg` — and, since there's no dedicated Amla photo, `ashwagandha-amla-lifestyle.jpg` is used for both the Ashwagandha section (cropped to the left, showing the roots) and the Amla section (cropped to the right, showing the berries). Article thumbnails reuse the same image cropped smaller rather than needing 18 separate photos.
  - **If you want a more editorial look later**, the two upgrades that would matter most: (1) a dedicated close-up photo of each raw botanical (turmeric root, ashwagandha root, jackfruit, amla berries, moringa leaves, hummingbird flower) shot against a soft neutral background rather than the product-bottle lifestyle shots — around **1000×1200px** (portrait) each; and (2) a bright, airy hero photo in the same spirit as `ingredients-bg.jpg` but with more open space on the right for the "Nature backed by science" caption — around **1600×1000px** (landscape). Neither is required; the page works fully with what's already in `images/`.
- Verified at desktop, tablet and mobile widths, tested the pill filter, search, and "View all" expand/collapse interactions, and re-ran the blog regression check — no errors (aside from the sandboxed Google Fonts request, which loads fine once live).

## Blog hero → full-bleed background + thumbnails hidden (2026-09-17)

- **Blog hero rebuilt as a full-bleed background** (matching the homepage/Science/Finder treatment) instead of the two-column layout from the previous round, using the botanical petri-dish/leaf photo you supplied (`images/blog-hero-bg.jpg`, saved at 1536×1024 — the same spec every other full-bleed image on the site uses). A light left-to-right gradient keeps the copy readable over the brighter part of the photo, and the "Nature backed by science." caption now sits bottom-right on desktop and stacks below the copy on mobile/tablet.
- **Article thumbnails are hidden for now** — the small 66×66px image slot next to each research article is still in the markup (so nothing has to be rebuilt), just switched off with a single CSS rule (`.article-thumb{display:none}` in the `<style>` block). When you're ready to add them, send the images (200–300px square works well) and I'll swap that one line back and drop the images in.
- Verified at desktop, tablet and mobile — fixed a stacking/positioning issue that appeared while adapting the caption for the mobile layout (it was briefly rendering behind the hero photo, then briefly mis-positioned off-screen) before confirming it displays cleanly at all three widths.

## Dedicated botanical spotlight photography added (2026-09-17)

- Replaced the reused product-lifestyle crops in each "Botanical Spotlight" panel with the 6 dedicated close-up photos you supplied (raw ingredient, soft neutral background, 1000×1200px portrait as requested): `images/black-turmeric-spotlight.jpg`, `images/ashwagandha-spotlight.jpg`, `images/jackfruit-spotlight.jpg`, `images/amla-spotlight.jpg`, `images/moringa-spotlight.jpg`, `images/hummingbird-spotlight.jpg`.
- Ashwagandha and Amla each now have their own distinct photo instead of sharing one crop of the combined product shot — the whole row now reads as pure, editorial botanical photography rather than product packaging.
- Article thumbnails are still hidden (unchanged from the last round) since these new images are the larger spotlight-panel size, not the 200–300px square thumbnail size — let me know if/when you'd like square crops made for those too.
- Verified at desktop and mobile, and re-ran the blog regression check — no errors.

## About page hero portrait added (2026-09-17)

- Replaced the "Portrait coming soon" placeholder in the About page hero with the real photo of Dr. Balasingham Arasabalan you supplied (`images/dr-balasingham-portrait.jpg`).
- Checked the crop before committing it: the source photo is a different aspect ratio than the `.about-photo` box (4/4.6), so I built a quick side-by-side render at the box's actual desktop and mobile sizes first to confirm `object-fit:cover` centers well with good headroom and no awkward cropping of his face or hands — confirmed good at both sizes.
- The Featured Research card's `.research-visual` placeholder is unchanged — still using the placeholder treatment, since that's a separate image slot from the hero portrait.
- Verified at desktop and mobile widths — no console/page errors.

## About page polish: portrait crop, frosted tag, and 2 more images (2026-09-17)

- **Portrait crop adjusted**: added `object-position:50% 20%` to the hero portrait so his head sits lower in the frame with more breathing room above it, instead of the default centered crop.
- **"Mind / Behaviour / Physiology / Health" tag box** now has a frosted-glass look — a semi-transparent navy background with `backdrop-filter: blur(10px)` and a soft white border, so the portrait shows through it softly instead of it being a flat solid block.
- **About Intro section**: replaced the reused `leaf-branch-1.png` in the decorative panel next to the bio copy with your dedicated image (`images/about-intro-leaf.jpg`, supplied at 1170×1345 — matches the size spec given earlier).
- **Featured Research card**: replaced the "Research imagery placeholder" box with your supplied image (`images/research-visual.jpg`, supplied at 1916×821 — a wide banner, cropped via `object-fit:cover` into the card's 170px-tall slot).
- Verified all three at desktop width and re-ran the shop.html regression suite — no errors.

## Research Philosophy section redesign (2026-09-17)

- Removed the short paragraph next to the pull-quote ("Clinical experience and scientific inquiry come together...") per your feedback.
- Reused the homepage's Science section background photo (`images/science-bg.jpg`) as a full-bleed background for this section, cropped with `object-position:center bottom` so it shows the rock/leaves/water reflection detail at the bottom of the image (the part you liked), rather than the plainer dark-blue upper portion.
- Switched the eyebrow, quote and attribution text to white/light-blue so they read clearly over the new dark photo background, and widened the vertical padding slightly so the quote has more breathing room against the image.
- Verified at desktop and mobile widths, and re-ran the shop.html and blog.html regression suites — no errors.

## WhatsApp/social link previews + SEO pass (2026-09-17)

**Link previews (WhatsApp, iMessage, Facebook, Slack, etc.)**
- The old setup wouldn't have shown a preview image reliably: `og:image` on the homepage pointed to a relative path (`images/...`), which most link-preview crawlers — including WhatsApp's — can't resolve, and `shop.html`, `blog.html` and `about.html` had no `og:image` at all.
- Designed **4 dedicated 1200×630px share cards** (the standard size social platforms crop to), one per page, each combining your logo, a page-specific headline, and a relevant photo: `images/share-home.jpg`, `images/share-shop.jpg`, `images/share-blog.jpg`, `images/share-about.jpg`. These looked cleaner and more on-brand than cropping an existing page photo down to the 1.91:1 ratio link previews expect.
- Every page now has a full set of Open Graph + Twitter Card tags with **absolute URLs** (`og:url`, `og:image` with width/height/alt, `twitter:image`, `og:site_name`) plus a `<link rel="canonical">` tag — this is what WhatsApp, iMessage, Slack and Facebook actually read to build a link preview.
- **One thing to know**: all the URLs used (`https://aaron-choice-website.pages.dev/...`) point at the current Cloudflare Pages address. If you move to a custom domain later, these need a find-and-replace to the new domain, or previews will keep pointing at the old one. Also, WhatsApp/Facebook cache previews aggressively — after deploying, test with Facebook's [Sharing Debugger](https://developers.facebook.com/tools/debug/) (paste the URL and click "Scrape Again") to force a refresh if an old/blank preview was already cached from an earlier share.

**SEO**
- **`sitemap.xml`**: was missing `about.html` entirely — added it, plus `lastmod` dates on all 4 URLs.
- **Structured data (JSON-LD)** added so Google can understand the site better and potentially show richer search results:
  - Homepage: `Organization` + `WebSite` schema.
  - Shop page: `Product` schema for all 7 products (name, image, description, price, availability) — this is what can make star ratings/prices show up directly in Google search results.
  - About page: `Person` schema for Dr. Balasingham Arasabalan (credentials, affiliation, areas of expertise).
  - **Note**: product prices in the schema are marked `CAD` based on the footer's "Proudly Canadian" line — confirm that's correct (vs. USD) before launch, and update `data-price` values too if not (there's already a note about this below for the 2 newest products).
- Audited all 4 pages: every image already has descriptive `alt` text, every page has exactly one `<h1>`, and all titles/meta descriptions are within Google's recommended length — no changes needed there.
- Existing `robots.txt` and per-page meta descriptions were already in decent shape from an earlier round and are unchanged.

## Shop page hero redesign (2026-09-17)

- **Rebuilt the Shop page hero** to match the reference layout you shared: a light cream section with the eyebrow ("The Aaron Choice Collection"), a large serif headline ("Botanical wellness, thoughtfully formulated."), copy, and an "Explore the Collection" button on the left, and your supplied hero photo (`images/shop-hero.jpg` — turmeric, moringa, amla and hibiscus on a stone slab) bleeding to the right edge of the page. The photo carries the italic "Nature / Research / Real Wellbeing" caption top-right and the "Traditional Botanicals / Modern Science / Brighter Tomorrows" caps list bottom-right, both with a soft white glow so they stay legible over the busy photo. A "Plants · Research · A Healthier Tomorrow" tagline sits in its own thin strip beneath, before the trust bar. Replaced the old plain centered text header (with breadcrumb) entirely.
- **Added the leaf panel to the product grid**: switched the grid from a fluid auto-fit layout to a fixed 4-columns-on-desktop grid (3 on tablet, 2 on small tablet, 1 on mobile), so the 7 products leave exactly one empty slot — filled with your supplied leaf image (`images/shop-leaf-panel.jpg`) and a "Small choices. A healthier tomorrow." message linking to the homepage's Ingredients section. The panel automatically hides when a wellness-goal filter narrows the results (since the "one gap" layout only makes sense on the full, unfiltered grid) and stays pinned as the last grid item when sorting.
- Verified at desktop, tablet and mobile widths, tested the filter/sort interactions with the new leaf panel, and re-ran the shop.html regression suite — no errors.

## About page: added name & professional title (2026-09-17)

- Added a name/title block in the About hero, between the eyebrow and headline: **"(Moses) A. Balasingham, PhD (PSY.), PhD (I-MD)"** with the subtitle **"Mental Health Consultant · Integrative & Functional Medical Practitioner"**.
- **Note**: the rest of the page (lead paragraph, Research Philosophy attribution, Featured Research byline, JSON-LD structured data, and the social share card) still refers to him as "Dr. Balasingham Arasabalan," per the original source document. If "(Moses) A. Balasingham" is now the name you want used site-wide, let me know and I'll update all of those to match.
- Verified at desktop and mobile widths, re-ran the shop.html regression suite — no errors.

## About page: added organization logo + name (2026-09-17)

- Below the new title line, added the Community Health & Preventive Care Inc. mark (`images/chpc-logo.png`) with "Community Health & Preventive Care Inc." next to it, in the About hero.
- Your supplied logo had a flat white background — removed it programmatically so it sits cleanly on the hero's pale background instead of showing a white box around it (same treatment used for the Aaron Choice logo in the nav).
- Verified at desktop and mobile widths, re-ran the shop.html regression suite — no errors.

## Shop hero → full-bleed single column, leaf panel text moved, Personalised Discovery added (2026-09-17)

- **Shop hero rebuilt as a single, full-bleed section**: the hero was a two-column layout (a light copy panel on the left, the photo confined to a separate column on the right). It's now one section — the photo covers the entire width, edge-to-edge, matching the full-bleed treatment used on the homepage/Blog heroes, with the cream-tinted gradient still fading left-to-right so the copy stays legible over the photo.
- **Leaf panel text moved up**: "Small choices. A healthier tomorrow." was anchored to the bottom of the panel, which could sit uncomfortably low once the card stretched to match the height of its taller neighbors in the grid row. Moved it to the top of the panel instead, with the gradient flipped (now a light fade from the top) to match.
- **Added the "Personalised Discovery" section** below the product grid — the same "Find your Aaron Choice" wellness finder from the homepage (background photo, eyebrow/heading/copy, "Browse All Products" button, and the working wellness-area dropdown + "Find my product" result), reusing `images/finder-bg.jpg`. The dropdown/button use their own ids (`shopGoal`, `findShopProduct()`) so they don't collide with the homepage's finder script.
- Verified at desktop and mobile widths, tested the finder's suggestion logic, and re-ran the shop.html regression suite — no errors.

## Trust bar mobile wrap fix + nav trust bar/pill mobile grid fixes (2026-09-19)

- **Trust bar** (`index.html` + `shop.html`) — the 5-item icon row wrapped raggedly on mobile. Fixed by switching each `.trust-item` to `flex-direction:column` (icon stacked above label, centered) with a smaller icon/font so labels fit on one line per cell.
- **Ingredient filter pills** on `blog.html` — same ragged-wrap problem, fixed with a 2-column CSS grid on mobile.

## Nav logo replaced (2026-09-19)

- Swapped `images/aaron-choice-logo.png` for Ann's new "Aaron Choice Canada" medallion logo (navy flat-top tab + circular badge with the sunrise/hands artwork, "Healing Begins Within", Psalm 104:14).
- The source file had a solid near-white background; ran a border-connected flood fill to knock it out to transparency, then trimmed to a tight bounding box (1218×1244) so the image edges match the artwork's own tag/medallion outline — same treatment the old logo file had.
- No CSS/markup changes needed — `.brand-mark` already scales by height and keeps the flat top pinned to `top:-24px` inside `.brand`, so the new logo hangs the same way (flat top tucked into the navy announcement bar, medallion poking down over the nav line). Same file is shared by all four pages' navs, so one image swap updated `index.html`, `shop.html`, `about.html`, and `blog.html` at once.
- Verified in headless screenshots at both mobile (390px) and desktop widths, and on shop/about (which share the same nav partial).

## Notes / things to swap before going live

- **Checkout**: the "Proceed to Checkout" button still shows an alert. Wire this to a real cart/checkout provider (Shopify, Stripe Checkout, Snipcart, etc.) before launch.
- **Search**: currently a simple client-side name filter over the products shown. If your catalogue grows or you want full-text/typo-tolerant search, connect a real search service.
- **Reviews**: sample testimonials are included; replace with verified customer reviews before launch (using placeholder names/quotes as if genuine is a legal risk once live).
- **Legal/compliance copy**: the FAQ and footer include notes flagging language that should be reviewed against your actual return policy, supplement regulations, and SKU-level claims before publishing.
- **Footer social links & newsletter**: the 5 footer social icons currently link to `#`, and the newsletter form just shows a "Subscribed!" confirmation toast. Point the social icons at your real profiles and wire the form up to an email service (Mailchimp, Klaviyo, etc.) before launch.
- **Domain in SEO/social tags**: canonical links, `og:url`, `og:image`, `twitter:image` and the sitemap all currently point at `https://aaron-choice-website.pages.dev`. If/when you connect a custom domain, do a find-and-replace across all 4 HTML files + `sitemap.xml` + `robots.txt` to the new domain, or search engines and link previews will keep referencing the old address.
- **Product schema currency**: the `Product` structured data on `shop.html` is marked `CAD` (based on the footer's "Proudly Canadian" line) — confirm this matches your actual pricing currency before launch.

## File structure

```
.
├── index.html    # the marketing homepage (HTML + CSS + JS inline)
├── shop.html     # the full retail Shop page (filter, sort, cart)
├── blog.html     # the research Blog, organized by ingredient
├── about.html    # About page — Dr. Balasingham Arasabalan profile
├── images/       # product photos and the "origin of disease" infographic
├── _headers      # Cloudflare Pages response headers
├── robots.txt
├── sitemap.xml
└── README.md     # this file
```
