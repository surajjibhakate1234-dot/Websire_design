# EMBER & OAK — Repository & Workspace Audit (Phase 0)

**Audit Date:** 2026-11-22  
**Workspace Path:** `d:\web_design`  
**Audit Status:** Complete for initial workspace state; **3D & Brand Asset audit pending file staging**

---

## 1. Workspace & Repository State

| Inspection Area | Initial Observation | Post-Phase 0 Action |
|---|---|---|
| Existing files & folders | **0 files, 0 folders** (completely empty directory) | Initialized Git, `.gitignore`, `README.md`, `docs/`, `assets/`, `blender/`, and `public/` skeleton |
| Git repository | Not initialized | Ran `git init` |
| Framework / `package.json` | None present | Scheduled for Phase 1 (`Next.js` + `React` + `TypeScript` + `Tailwind CSS`) |
| Reusable code / components | None present | Greenfield modular monolith |
| Database / Supabase config | None present | Scheduled for Phase 1 (`supabase/migrations/` & `supabase/seed.sql`) |

---

## 2. Local Development Toolchain Audit

| Tool | Status | Observed Version / Notes |
|---|---|---|
| Node.js | Available | `v24.16.0` |
| npm | Available | `11.13.0` (recommended default package manager) |
| Git | Available | Installed and initialized |
| pnpm | Not installed | `pnpm` not recognized on `PATH` |
| Blender | Not found on `PATH` | `where.exe blender` returned no matches. Required before Phase 3 if raw 3D assets include `.blend`, `.fbx`, or `.obj` files requiring conversion or decimation; Node-based `@gltf-transform/cli` can inspect and optimize `.glb`/`.gltf` directly |
| Python | Unavailable in sandbox | Windows Store stub could not execute |

---

## 3. Downloaded 3D Assets Audit

- **Location Checked:** `d:\web_design` (recursive)
- **Assets Found:** **0**
- **Impact:** Critical blocker for finalizing `docs/3d-asset-manifest.md` and Phase 3 scene engineering. Per Section 5 of the Master Blueprint, generic placeholder models must **not** replace existing downloaded assets.
- **Action Required:** Copy (preserving originals) all downloaded 3D models (`.glb`, `.gltf`, `.fbx`, `.obj`, `.blend`, `.usdz`), texture maps (`.png`, `.jpg`, `.webp`, `.exr`, `.hdr`), and source license files into:
  - `assets/original/` — raw downloaded models and textures
  - `assets/licenses/` — attribution, license text, receipts, or source URLs

---

## 4. Brand Assets Audit

- **Assets Found:** **0** (no logo, brand book, typography license, or real café photography present in workspace)
- **Impact:** Visual tokens (Espresso brown, Oat cream, Terracotta, Muted olive, Honey) and copy will remain explicitly marked as `[PLACEHOLDER]` / provisional until owner brand assets are staged in `assets/reference/` and reviewed.

---

## 5. Identified Risks & Mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| Downloaded 3D assets not yet in workspace | **High** | Stage files into `assets/original/` before Phase 3; keep Phases 1–2 commerce-first so development is not blocked |
| Non-GLB 3D formats without Blender on `PATH` | **Medium** | Verify file formats upon staging; install/locate Blender if `.blend`/`.fbx`/`.obj` conversion is needed |
| Missing license documentation for 3D assets | **High** | Record source & license status per asset in `docs/3d-asset-manifest.md`; reject/replace unverified assets before launch |
| Unconfirmed Supabase & Payment provider credentials | **Medium** | Build provider-agnostic adapters and local migrations/seed data first; wire sandbox credentials in Phase 4–5 |
| Missing real menu, GST, hours, and legal policies | **High (Launch)** | Track all 18 required items in `docs/owner-information-required.md`; tag all temporary values `[PLACEHOLDER]` |

---

## 6. Recommended Next Steps

1. **Owner:** Stage downloaded 3D files into `assets/original/`, licenses into `assets/licenses/`, and logos/café photos into `assets/reference/` whenever ready.
2. **Engineering (Phase 1):** Initialize Next.js + TypeScript + Tailwind CSS + ESLint + Vitest, establish the provisional EMBER & OAK design system, write core money (`paise`) & time (`UTC/IST`) utilities with unit tests, and author the Phase 1 Supabase schema migrations and RLS policies.
