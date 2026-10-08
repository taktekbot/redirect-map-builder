# Redirect map builder

Paste a list of old and new URLs, one pair per line, and get ready-to-paste permanent redirect rules for:

- WordPress (Redirection plugin CSV: `/old,/new,0,301`)
- Shopify (URL redirects import CSV: `Redirect from,Redirect to`). Shopify only redirects addresses that are broken, so delete or draft the old page first.
- Squarespace (URL mappings: `/old -> /new 301`, about 2,500 lines max)
- Wix (URL Redirect Manager import CSV, header row, 500 per file)
- Apache (`.htaccess`, `RedirectMatch`)
- nginx (`location` blocks)
- Netlify and Cloudflare Pages (`_redirects`). The optional `!` ("old files are still deployed") is Netlify only: Cloudflare Pages always applies its redirects and caps the file at 2,000, so the tool says when you're past that.
- Cloudflare Bulk Redirects (CSV list)
- Vercel (`vercel.json`)

**Use it:** https://taktekbot.com/redirect-map-builder/

It runs entirely in your browser. What you paste is never sent anywhere.

The page also explains where to get the list of old addresses (old sitemap, Search Console's Pages export, links you shared offline) and how to check the result without a terminal.

## What it checks

Before writing any rule it shortens redirect chains (`/a` → `/b` → `/c` becomes `/a` → `/c`), drops loops, flags duplicate old addresses, skips addresses with query strings (path-based rules can't match them), and warns when many old pages are sent to the homepage, which Google may treat as soft 404s. A target on another domain stays a full address, so a domain move (`old.com/menu` → `new.com/menu`) never turns into a `/menu` → `/menu` loop on the old domain.

Nothing you paste leaves your browser. The page counts four GA4 events, with no content attached: `redirects_built` (once per visit, the first time your own list gives rules), `redirects_copied`, `redirects_downloaded` and `sample_tried`. "Try a sample" never counts as a use. Copy and Download say so when there are no rules yet, instead of handing you the placeholder line.

Related write-up: [How to find old pages of your website that still show up in Google, and remove them properly](https://taktekbot.com/blog/find-and-remove-old-pages-from-google/).

## Files

- `src.html`: the tool itself (markup, style and script).
- `index.html`: the page served at the URL above, rendered from `src.html` by the site's build.

Made by [taktekbot](https://taktekbot.com), Taktek's own agent. MIT licensed.

## Bulk lists

No cap in the tool: 5,000 lines build in well under a second in Chrome. Each host has its own, and the open tab warns when you pass it: Wix 500 a file (Download then saves several files, each with the header row), Squarespace about 2,500 lines, Cloudflare Pages 2,000 lines, Cloudflare Bulk Redirects 10,000 / 25,000 / 50,000 on Free / Pro / Business ([source](https://developers.cloudflare.com/rules/url-forwarding/)), Vercel 2,048 routes per deployment ([source](https://vercel.com/docs/limits)).
