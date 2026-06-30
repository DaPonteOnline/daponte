# Da Ponte Online — deploy artifact

**Generated, do not hand-edit.** This repository holds the *built* static site
(HTML/CSS/JS + IIIF facsimiles + Pagefind search index) produced from the
source repository. To change the site, edit the source and rebuild — never edit
files here directly; they will be overwritten on the next deploy.

- **Source repo:** `da_ponte` (the Astro project)
- **Target host:** Unibo DHARC (static web server, Apache assumed)
- **Runtime required:** none. Pure static files.

## How this artifact was built

```bash
# from the source repo
SITE_URL="https://YOUR_DHARC_HOST_HERE" BASE_PATH="/" THEME=default npm run build
# then dist/ was copied here
```

⚠️ **Placeholders — rebuild before going live on Dharc.**
This snapshot was built with:
- `BASE_PATH=/`  → assumes the site is mounted at the **domain root**.
- `SITE_URL=https://YOUR_DHARC_HOST_HERE` → only affects absolute URLs in
  `<link rel="canonical">`, Open Graph tags, and the sitemap.

If Dharc serves the site at a **sub-folder** (e.g. `https://dharc.unibo.it/daponte/`),
you **must** rebuild — the base path is baked into every internal link at build
time and cannot be patched afterward:

```bash
SITE_URL="https://dharc.unibo.it" BASE_PATH="/daponte" THEME=default npm run build
```

Then resync `dist/` into this repo and update the `ErrorDocument` line in
`.htaccess` to `/daponte/404.html`.

## Server requirements (Apache — see `.htaccess`)

1. **`DirectoryIndex index.html`** — serve `index.html` for directory URLs.
2. **`AddType application/wasm .wasm`** — Pagefind search is WebAssembly; wrong
   MIME = broken search.
3. **`ErrorDocument 404`** — point at `404.html` (root) or `<base>/404.html`.

On nginx, the equivalents are `index index.html;`, a `types { application/wasm wasm; }`
entry, and `error_page 404 /404.html;`.

## Notes

- `.nojekyll` is present so this also works unmodified if ever served via
  GitHub Pages (Jekyll would otherwise skip the `_astro/` directory).
- "View TEI source" links point at the canonical GitHub source repo by design;
  they are absolute and host-independent.
