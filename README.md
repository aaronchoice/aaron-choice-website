# Aaron Choice — Website

A static site for Aaron Choice (premium botanical supplements): a one-page storefront (`index.html`) plus a research Blog (`blog.html`). Pure HTML/CSS/JS, no build step, no dependencies.

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

## Notes / things to swap before going live

- **Product images**: three of four still point to a Wix CDN and one to an Unsplash stock photo — these are hotlinked from someone else's infrastructure and could break or get rate-limited without warning. Replace with your own hosted product photography.
- **Checkout**: the "Proceed to Checkout" button still shows an alert. Wire this to a real cart/checkout provider (Shopify, Stripe Checkout, Snipcart, etc.) before launch.
- **Search**: currently a simple client-side name filter over the four products shown. If your catalogue grows or you want full-text/typo-tolerant search, connect a real search service.
- **Reviews**: sample testimonials are included; replace with verified customer reviews before launch (using placeholder names/quotes as if genuine is a legal risk once live).
- **Legal/compliance copy**: the FAQ and footer include notes flagging language that should be reviewed against your actual return policy, supplement regulations, and SKU-level claims before publishing.

## File structure

```
.
├── index.html    # the storefront (HTML + CSS + JS inline)
├── blog.html     # the research Blog, organized by ingredient
├── images/       # product photos and the "origin of disease" infographic
├── _headers      # Cloudflare Pages response headers
├── robots.txt
├── sitemap.xml
└── README.md     # this file
```
