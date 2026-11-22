# EMBER & OAK — Implementation Roadmap & Backlog

**Last Updated:** 2026-11-22  
**Current Milestone:** Phase 0 Complete → Ready for Phase 1

---

## Phase Tracker

| Phase | Scope | Target Est. | Status | Exit Gate |
|---|---|---|---|---|
| **Phase 0** | Workspace audit, repo skeleton, baseline docs & asset manifest setup | 2–4 days | **Completed (Asset audit pending file staging)** | 6 docs authored; workspace & toolchain audited |
| **Phase 1** | Next.js + TS + Tailwind setup, provisional design system, money/time libs, initial Supabase migrations & RLS | 3–5 days | **Next** | App runs locally; lint, typecheck, unit tests & build pass |
| **Phase 2** | Responsive customer storefront (Home, Menu, Product Detail, About, Visit) + read APIs | 4–7 days | Pending | Full mobile/desktop menu browsing without 3D |
| **Phase 3** | 3D asset processing, R3F hero scene, guided camera, interactive hotspots & WebGL fallback | 3–7 days | Pending (requires staged 3D assets) | 3D approved; WebGL fallback works; mobile perf verified |
| **Phase 4** | Supabase Auth, server RBAC, Admin Dashboard, Menu/Modifier CRUD, Order Queue & Kitchen Display | 6–10 days | Pending | Owner manages menu & orders without code changes |
| **Phase 5** | Persistent Cart, server-side pricing/GST, Checkout, sandbox Payment webhooks & Reservations | 4–8 days | Pending | E2E sandbox purchase & conflict-free reservation tests pass |
| **Phase 6** | Café-owned & 3rd-party delivery, ingredient inventory ledger, analytics, optional Loyalty/Accounts | 5–10 days | Pending | Approved operational modules verified in staging |
| **Phase 7** | Unit, Integration, Playwright E2E, Security/RLS review, Accessibility & Lighthouse optimization | 4–6 days | Pending | Zero critical/high launch blockers |
| **Phase 8** | Production Vercel + Supabase setup, domain/HTTPS, backups, monitoring, runbook & handover | 2–4 days | Pending | Production smoke tests pass & owner signs off |
| **Phase 9** | Post-launch stabilization, webhook/error/3D monitoring & funnel refinement | 2 weeks | Pending | Stable production metrics & prioritized v1.1 backlog |

---

## Strict Implementation Sequence (First 7 Core Milestones)

Per Blueprint Section 16, foundational customer value is delivered in this exact order before expanding to full commercial operations:

1. **Workspace & Asset Audit** (`Phase 0` — workspace done; re-run asset scan as soon as files are placed in `assets/original/`).
2. **Application Foundation** (`Phase 1` — Next.js App Router, strict TS, Tailwind, Zod, Vitest, Supabase schema).
3. **Design System** (`Phase 1` — Espresso/Oat/Terracotta/Olive/Honey tokens, editorial typography, accessible UI primitives).
4. **Basic Responsive Homepage** (`Phase 2` — fast initial paint with static hero fallback and clear CTAs).
5. **One Optimized 3D Café Hero Scene** (`Phase 3` — lazy-loaded R3F scene built from audited assets in `assets/original/`).
6. **One Working Menu Hotspot** (`Phase 3` — interactive 3D menu board hotspot + keyboard-accessible navigation control linking to `/menu`).
7. **Real Menu/Catalog Data Structure** (`Phase 1–2` — PostgreSQL categories, products, variants, modifier groups, availability, integer paise pricing).

Once milestones 1–7 are verified, proceed sequentially into **Admin & KDS (Phase 4)**, **Checkout/Payments/Reservations (Phase 5)**, **Delivery & Inventory (Phase 6)**, **QA/Hardening (Phase 7)**, and **Production Launch (Phase 8–9)**.
