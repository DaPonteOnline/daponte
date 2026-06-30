# Da Ponte Online — deploy artifact

**Generated, do not hand-edit.** This repository holds the *built* static site
(HTML/CSS/JS + IIIF facsimiles + Pagefind search index) produced from the
source repository. To change the site, edit the source and rebuild — never edit
files here directly; they will be overwritten on the next deploy.

- **Source repo:** `da_ponte` (the Astro project)
- **Target host:** `https://daponte.ficlit.unibo.it` (Unibo DHARC, Apache assumed)
- **Mount point:** domain **root** of the subdomain (`BASE_PATH=/`)
- **Runtime required:** none. Pure static files.

## How this artifact was built

```bash
# from the source repo
SITE_URL="https://daponte.ficlit.unibo.it" BASE_PATH="/" THEME=default npm run build
# then dist/ was copied here (rsync), preserving .htaccess / DEPLOY.md / .nojekyll
```

Because the site lives on its own subdomain, it is mounted at the root, so
`BASE_PATH=/` is correct and every internal link is root-relative. If the mount
point ever changes to a **sub-folder** (e.g. `…/daponte/`), you **must** rebuild
— the base path is baked into every internal link at build time and cannot be
patched afterward:

```bash
SITE_URL="https://daponte.ficlit.unibo.it" BASE_PATH="/daponte" THEME=default npm run build
```

…and then update the `ErrorDocument` line in `.htaccess` to `/daponte/404.html`.

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
