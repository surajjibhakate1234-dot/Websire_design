# EMBER & OAK — 3D Asset Manifest & License Register

**Last Updated:** 2026-11-22  
**Assets Inspected:** 0  
**Assets Ready for Integration:** 0  
**Raw Staging Directory:** `assets/original/`  
**Runtime Output Directory:** `public/models/`

> **Policy:** Original downloaded files in `assets/original/` must never be overwritten or deleted. Never fabricate license approvals. Only audited, optimized, and license-confirmed assets may be exported to `public/models/` for production.

---

## 1. Status Definitions

- `Not inspected` — File discovered in `assets/original/`, not yet analyzed.
- `Inspected` — Format, file size, dimensions, polycount, textures, orientation, and animations recorded.
- `License confirmed` — Commercial web usage rights verified and documented in `assets/licenses/`.
- `Requires optimization` — Needs geometry decimation, scale/pivot normalization, texture compression, or GLB conversion.
- `Ready for integration` — Optimized `.glb`/`.gltf` validated in browser and placed in `public/models/`.
- `Rejected` — Unsuitable geometry, broken materials, or unverified/incompatible license.

---

## 2. Asset Inventory

| Asset Filename | Format | Raw Size | Polycount / Dimensions | Textures & Materials | Animations | Scale / Orientation | License & Source | Intended Website Usage | Runtime Path | Status |
|---|---|---|---|---|---|---|---|---|---|---|
| *(No files currently staged in `assets/original/`)* | — | — | — | — | — | — | — | — | — | Pending staging |

---

## 3. Target Hero Scene Asset Slots (Blueprint Section 4)

Once downloaded assets are staged in `assets/original/`, map each asset to one of the target scene roles below before deciding whether any supplementary asset is needed:

| Scene Slot / Hotspot | Planned Interaction | Mapped Asset | Status |
|---|---|---|---|
| Café Entrance / Shell | Framing & spatial atmosphere | TBD | Awaiting asset staging |
| Café Signage | Return to homepage (`/`) | TBD | Awaiting asset staging |
| Menu Board | Open menu (`/menu`) | TBD | Awaiting asset staging |
| Hero Coffee Cup | Open featured product (`/menu/[slug]`) | TBD | Awaiting asset staging |
| Pastry Display | Open bakery category (`/menu?category=bakery`) | TBD | Awaiting asset staging |
| Indoor Seating | Open reservation with indoor preference (`/reservations?zone=indoor`) | TBD | Awaiting asset staging |
| Outdoor Seating | Open reservation with outdoor preference (`/reservations?zone=outdoor`) | TBD | Awaiting asset staging |
| Wall Artwork / Decor | Open brand story (`/about`) | TBD | Awaiting asset staging |
| Static Fallback Poster | Shown while 3D loads or when WebGL is disabled | `public/posters/hero-fallback.webp` | To generate/capture in Phase 3 |

---

## 4. Asset Preparation Checklist (Phase 3)

For every asset promoted from `assets/original/` to `public/models/`:
1. Verify commercial license and store proof in `assets/licenses/`.
2. Copy working file to `assets/processed/` (never edit `assets/original/`).
3. Remove hidden/unused meshes and fix missing texture references.
4. Normalize units (1 unit = 1 meter, Y-up, origin at floor/base).
5. Decimate excessive geometry and merge draw calls where materials match.
6. Resize textures appropriately (max 1024px–2048px for hero, 512px–1024px for props) and compress (WebP / KTX2-Basis).
7. Export to `.glb` with Draco compression (only after confirming materials and animations are preserved).
8. Validate rendered appearance, lighting, and download budget in desktop & mobile browsers.
