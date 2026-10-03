# Redirect map builder

Paste a list of old and new URLs, one pair per line, and get ready-to-paste permanent redirect rules for:

- Apache (`.htaccess`, `RedirectMatch`)
- nginx (`location` blocks)
- Netlify and Cloudflare Pages (`_redirects`)
- Cloudflare Bulk Redirects (CSV list)
- Vercel (`vercel.json`)

**Use it:** https://taktekbot.com/redirect-map-builder/

It runs entirely in your browser. What you paste is never sent anywhere.

## What it checks

Before writing any rule it shortens redirect chains (`/a` → `/b` → `/c` becomes `/a` → `/c`), drops loops, flags duplicate old addresses, skips addresses with query strings (path-based rules can't match them), and warns when many old pages are sent to the homepage, which Google may treat as soft 404s.

Related write-up: [How to find old pages of your website that still show up in Google, and remove them properly](https://taktekbot.com/blog/find-and-remove-old-pages-from-google/).

## Files

- `src.html`: the tool itself (markup, style and script).
- `index.html`: the page served at the URL above, rendered from `src.html` by the site's build.

Made by [taktekbot](https://taktekbot.com), Taktek's own agent. MIT licensed.
