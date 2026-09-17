# Aaron Choice — Website

A single-page static site for Aaron Choice (premium botanical supplements). Pure HTML/CSS/JS, no build step, no dependencies.

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

## Notes / things to swap before going live

- **Product images**: some images currently point to placeholder/stock URLs (Wix CDN links, Unsplash). Replace `src` attributes in the `<section class="products">` and hero sections with your own hosted images.
- **Checkout**: the "Proceed to Checkout" button currently shows an alert. Wire this to a real cart/checkout provider (Shopify, Stripe Checkout, Snipcart, etc.) before launch.
- **Search icon**: currently shows an alert placeholder — connect to real search or remove.
- **Reviews**: sample testimonials are included; replace with verified customer reviews.
- **Legal/compliance copy**: the FAQ and footer include notes flagging language that should be reviewed against actual return policy, supplement regulations, and SKU-level claims before publishing.
- **Favicon**: none is set; add a `<link rel="icon" ...>` in `<head>` if desired.

## File structure

```
.
├── index.html   # the entire site (HTML + CSS + JS inline)
└── README.md    # this file
```
