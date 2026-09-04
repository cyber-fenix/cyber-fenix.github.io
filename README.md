# cyber-fenix.github.io

The CyberFenix website — a static site served by GitHub Pages at
<https://cyber-fenix.github.io/>.

No build step, no dependencies, no JavaScript. Edit the HTML, push to `main`,
and GitHub publishes it within a minute or two.

## Local preview

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening the `.html` files directly with `file://` also works, apart from the
404 page (its links are absolute).

## Structure

```
index.html                                 home
products/gmail-bulk-extractor/index.html   product page
privacy/index.html                         privacy policy — required by the Web Store
support/index.html                         troubleshooting + billing help
404.html
assets/css/site.css                        the entire stylesheet
assets/img/                                logo, icons, screenshots (see its README)
robots.txt · sitemap.xml
.nojekyll                                  serve files as-is, no Jekyll processing
```

Every page is self-contained: header, footer and `<head>` are repeated in each
file rather than templated. With four pages that is the cheaper trade — no
generator to install, nothing to break at deploy time. If the site grows past
roughly ten pages, revisit that.

Links are relative, so the site works at a GitHub Pages subdomain, at a custom
domain, or from a local folder without changes.

## Before publishing — checklist

1. **Chrome Web Store link.** Every "Add to Chrome" button points at a
   placeholder. Once the extension is live, replace it everywhere:
   ```sh
   grep -rl REPLACE_ME . | xargs sed -i '' \
     's|https://chrome.google.com/webstore/detail/REPLACE_ME|<your real store URL>|g'
   ```
2. **Screenshots.** Replace the five grey placeholders in `assets/img/` — see
   [`assets/img/README.md`](assets/img/README.md) for the shot list and sizes.
3. **Pricing.** No price is stated anywhere on the site. Add it to the product
   page's plans section once it is fixed.

Settled, but re-check if either changes:

- **Trial length** — the site says **3 days**, matching `TRIAL_DAYS` in the
  extension's `src/lib/license.ts`. Change both together; it is a public promise.
- **Support address** — `cyberfenix.dev@gmail.com`, on the support and privacy pages.

## Adding a product

1. Copy `products/gmail-bulk-extractor/` to `products/<new-product>/` and rewrite
   the copy. Path depth is the same, so the relative links still resolve.
2. Add a `<article class="card">` to the product grid in `index.html`.
3. Add the product's icon to `assets/img/` and its URL to `sitemap.xml`.
4. If the product handles data differently, extend the privacy policy — it is
   written to cover all CyberFenix extensions, not just this one.

## Custom domain

When a domain is registered:

1. Add a file named `CNAME` at the repository root containing just the hostname,
   e.g. `cyberfenix.com`.
2. At the DNS provider, point the apex at GitHub Pages
   (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`) and add a `www`
   `CNAME` to `cyber-fenix.github.io`.
3. In the repo's Settings → Pages, set the custom domain and enable
   **Enforce HTTPS**.
4. Update the absolute URLs in each page's `<link rel="canonical">` and
   `og:*` tags, plus `robots.txt` and `sitemap.xml`.

## Licence

Site content © CyberFenix. The extensions it describes are open source under the
MIT licence.
