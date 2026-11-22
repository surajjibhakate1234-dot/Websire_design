# EMBER & OAK — Immersive 3D Café Website & Commercial Platform

**Tagline:** Your everyday pause.  
**Market:** India | **Currency:** INR (₹) | **Model:** Single-location artisan café

---

## Project Status

- **Current Phase:** Phase 0 — Discovery, Workspace Audit & Documentation
- **Next Milestone:** Asset staging (`assets/original/` & `assets/reference/`) and Phase 1 — Project Foundation, Design System & Core Schema

## Architecture Overview

EMBER & OAK is built as a modular monolith using:
- **Application:** Next.js (App Router), React, TypeScript, Tailwind CSS
- **3D Layer:** Three.js, React Three Fiber, Drei, GSAP (strictly presentation-only; progressive enhancement with static fallback)
- **Backend & Data:** Supabase (PostgreSQL with Row Level Security, Supabase Auth, Supabase Storage), Zod validation, server-side services
- **Testing:** Vitest (unit/integration) & Playwright (end-to-end)

## Key Documentation

| Document | Purpose |
|---|---|
| [Master Blueprint](docs/master-blueprint.md) | Complete product specification and engineering rules (v1.0) |
| [Repository Audit](docs/repository-audit.md) | Phase 0 workspace, asset, and toolchain audit findings |
| [3D Asset Manifest](docs/3d-asset-manifest.md) | Asset inventory, technical metrics, license register, and readiness status |
| [Architecture](docs/architecture.md) | System boundaries, data invariants (paise/UTC), security, and API overview |
| [Implementation Roadmap](docs/implementation-roadmap.md) | Phase 0–9 backlog, dependencies, and exit criteria |
| [Owner Information Required](docs/owner-information-required.md) | Checklist of 18 real café details required before production launch |

## Staging Downloaded 3D & Brand Assets

Before Phase 3 (3D integration) and finalizing visual design tokens:
1. Copy (do not destructively move) raw downloaded 3D files and textures into `assets/original/`.
2. Copy license files, invoices, or source attributions into `assets/licenses/`.
3. Copy official logo files and real café photographs into `assets/reference/`.
4. Only optimized runtime assets (`.glb`/`.gltf`, compressed textures, poster images) will be placed in `public/`.
