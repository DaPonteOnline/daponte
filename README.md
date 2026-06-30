# Da Ponte Online — A Digital Scholarly Edition (Web Application)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21083489.svg)](https://doi.org/10.5281/zenodo.21083489)

The published web-app form of the **Da Ponte** digital scholarly edition of
late-17th–18th-century Italian libretti: libretto reading views with facing
facsimiles, a three-way intertextual comparator for *Il Talismano*, a character
relationship network, and client-side full-text search.

**Live site:** <https://daponte.ficlit.unibo.it>

## What this deposit contains

The rendered, static, **re-hostable** site — HTML/JS/CSS, IIIF facsimile tiles,
and the Pagefind search index. No server runtime is required; it can be served
from any static web host, or re-served directly from this archive.

## License

Released under **[CC BY 4.0](LICENSE)** (Creative Commons Attribution 4.0
International). Bundled third-party libraries (the Astro/Svelte runtime,
Pagefind, etc.) retain their own licenses.

## How to cite

See [`CITATION.cff`](CITATION.cff). Cite the **version** you consulted, and the
**concept DOI** (all versions) in the bibliography:

- **Concept DOI (all versions):** [10.5281/zenodo.21083489](https://doi.org/10.5281/zenodo.21083489)
- **This version (v0.1.1):** [10.5281/zenodo.21083641](https://doi.org/10.5281/zenodo.21083641)

## Related deposits & source

- **TEI editions** (the encoded libretti) are archived separately:
  [10.5281/zenodo.21082557](https://doi.org/10.5281/zenodo.21082557).
- **Source code** (the Astro project this site is built from):
  <https://github.com/mary-lev/DaPonte>.

## Deployment

This repository is also the deployment artifact for the live site. Server setup
and update instructions are in [`DEPLOY.md`](DEPLOY.md).
