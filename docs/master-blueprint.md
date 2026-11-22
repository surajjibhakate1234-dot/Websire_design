# EMBER & OAK
# IMMERSIVE 3D CAFÉ WEBSITE & COMMERCIAL PLATFORM
## Master Development Blueprint — Version 1.0

**Product:** EMBER & OAK  
**Tagline:** Your everyday pause.  
**Market:** India  
**Currency:** INR (₹)  
**Business model:** Single-location café  
**Document purpose:** Product specification, technical architecture, development roadmap, implementation instructions and deployment guide.

---

# 1. PROJECT OVERVIEW

## 1.1 Vision

Develop a premium, immersive, 3D café website for EMBER & OAK that connects the atmosphere of a physical café with a fully functional digital business platform.

The website should give customers the feeling of entering and exploring a real café while allowing them to browse products, customize orders, make payments, reserve tables and interact with the brand.

The platform must also provide the café owner with a secure administration system to manage products, orders, customers, reservations, inventory, staff and daily operations.

The result should be a complete digital café ecosystem, not merely a promotional website or 3D visual showcase.

## 1.2 Core Objectives

1. Create a distinctive premium café identity online.
2. Build an immersive and interactive 3D website experience.
3. Integrate the already-downloaded 3D assets.
4. Develop a fully functional menu and ordering system.
5. Implement secure checkout and payment processing.
6. Enable reservations and order tracking.
7. Provide an owner-facing management dashboard.
8. Support café-owned delivery and third-party delivery integrations.
9. Build a scalable foundation for future business features.
10. Deploy a secure, responsive, production-ready website.

## 1.3 Product Principles

- **Brand authenticity:** Visual design should reflect the real café and its actual brand assets.
- **Commerce first:** Customers must be able to order without interacting with 3D.
- **Progressive enhancement:** Load the website first and 3D elements when required.
- **Mobile first:** Optimize the experience for phones, not just desktop screens.
- **Owner autonomy:** Routine business changes should not require code deployments.
- **Security:** Business-critical calculations and permissions must be enforced server-side.
- **Performance:** 3D must not compromise navigation, ordering or checkout.
- **Maintainability:** Use modular architecture and documented business logic.

---

# 2. BRAND IDENTITY AND VISUAL DIRECTION

## 2.1 Brand Identity

EMBER & OAK represents a contemporary artisan café focused on coffee, comfort, creativity and everyday experiences.

Brand personality: Warm, Contemporary, Refined, Minimal, Artisan, Welcoming, Premium but approachable.

Tagline: **Your everyday pause.**

## 2.2 Visual Direction (Provisional — Pending Owner Brand Asset Inspection)

| Color | Suggested Use |
|---|---|
| Espresso brown | Primary brand color |
| Oat cream | Main background |
| Terracotta | Accent color |
| Muted olive | Secondary accent |
| Honey | Highlights |
| Walnut and oak | 3D materials and textures |

Materials and atmosphere: Natural oak and walnut, brass accents, stone and textured surfaces, warm daylight, soft shadows, contemporary furniture, artisan coffee equipment.

Do not finalize the visual system until the available café photographs, logo, brand materials and downloaded 3D assets have been inspected.

## 2.3 Typography and UI

Refined editorial design system with distinctive display typography, highly readable body typography, consistent spacing, responsive grids, clear navigation, accessible buttons/forms, consistent product cards, subtle transitions, and restrained animations.

---

# 3. PRODUCT SCOPE

## 3.1 Customer-Facing Website

| Page | Main Functionality | Priority |
|---|---|---|
| Homepage | Brand presentation and immersive 3D experience | MVP |
| Menu | Categories, products, filters and availability | MVP |
| Product details | Images, descriptions, variants and add-ons | MVP |
| Cart | Item management and pricing | MVP |
| Checkout | Customer details, fulfilment and payment | MVP |
| Order confirmation | Order reference and status | MVP |
| Order tracking | Preparation and fulfilment updates | MVP |
| Reservations | Date, time, guest count and seating preference | MVP |
| About | Brand story and café atmosphere | MVP |
| Visit/contact | Address, hours and contact details | MVP |
| Customer account | Profile, saved addresses and order history | Phase 2 |
| Loyalty | Points and rewards | Phase 2 |

## 3.2 Admin Platform

Dashboard, Orders, Kitchen, Menu, Modifiers, Availability, Reservations, Customers, Promotions, Content, Inventory, Delivery, Staff, Analytics, Settings.

## 3.3 User Roles

- **Owner:** Full platform access.
- **Manager:** Business operations and management.
- **Staff:** Authorized order and customer operations.
- **Kitchen:** Preparation queue and order updates.
- **Delivery staff:** Assigned delivery information.
- **Customer:** Personal account and order information.

All permissions must be checked on the server.

---

# 4. 3D WEBSITE EXPERIENCE

- Suggested environment zones: Entrance, Coffee counter, Indoor seating, Outdoor seating, Featured product display.
- Prioritize one polished 3D hero experience in initial release.
- Interactive hotspots: Café signage (Homepage), Menu board (Menu), Coffee cup (Featured product), Pastry display (Bakery category), Indoor seating (Reservation — indoor), Outdoor seating (Reservation — outdoor), Artwork (Brand story).
- All hotspots must remain accessible via conventional navigation and mobile-friendly controls.
- Behaviors: Smooth guided camera transitions, lazy loading, loading indicators, static fallback images, reduced-motion support, WebGL failure handling, mobile optimization, pause when hidden/inactive.
- Performance targets: LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1 (measured, not assumed).

---

# 5. DOWNLOADED 3D ASSET INTEGRATION

- Preserve original files in `assets/original/`; process in `assets/processed/`; serve only optimized runtime assets in `public/`.
- Maintain `docs/3d-asset-manifest.md` with explicit statuses: `Not inspected`, `Inspected`, `License confirmed`, `Requires optimization`, `Ready for integration`, `Rejected`.
- Never replace suitable downloaded assets with generic models; never invent license approval.

---

# 6. CUSTOMER JOURNEYS AND BUSINESS LOGIC

- **Ordering flow:** Homepage → Menu → Product → Customize → Cart → Checkout → Payment → Confirmation → Preparation → Fulfilment.
- **Server-side authority:** Never trust frontend totals or frontend payment-success redirects.
- **Order lifecycle:** `Pending Payment → Confirmed / Placed → Accepted → Preparing → Ready → (Pickup: Completed | Delivery: Out for Delivery → Completed)`, plus separate `Cancelled`, `Rejected`, `Payment Failed`, and `Refunded` states with immutable status history.
- **Payments:** Provider-independent adapter (Razorpay candidate pending owner selection), server-side creation, signed webhook verification, idempotency, failure handling, refunds, reconciliation, zero card/CVV storage.
- **Reservations:** Server-side availability respecting opening hours, capacity, existing bookings, duration, buffer, blackouts, cutoff rules, and conflict-free database transactions.
- **Delivery:** Both café-owned delivery and pluggable third-party delivery interface.
- **Inventory & Loyalty:** Append-only auditable ledgers (`stock_movements`, `loyalty_transactions`) rather than direct balance mutation.

---

# 7. TECHNICAL ARCHITECTURE & DATABASE RULES

- **Stack:** Next.js, React, TypeScript, Tailwind CSS, Three.js, React Three Fiber, Drei, GSAP, PostgreSQL (Supabase), Supabase Auth & Storage, Zod, Zustand, Vitest, Playwright, Blender, Vercel.
- **Architecture:** Modular monolith; business logic separated from UI; 3D layer strictly presentation-only.
- **Data rules:** INR stored in integer **paise** (₹150 = 15000); timestamps stored in **UTC** and displayed in configured café timezone (`Asia/Kolkata`); immutable historical order-item price snapshots; archive instead of deleting historically referenced products; foreign keys, indexes, and PostgreSQL Row Level Security (RLS).

---

# 8. PROJECT RULES & GOVERNANCE

1. Inspect existing workspace before creating files; never assume empty or assume GLB/glTF format.
2. Preserve original asset files; check suitability and licensing.
3. Never invent real café information; use clearly marked `[PLACEHOLDER]` content until owner approval.
4. Keep business logic separate from UI and 3D separate from commerce.
5. Validate all commercial operations and admin permissions server-side.
6. Write tests alongside implementation; run lint, typecheck, tests, and build after each phase.
7. Never commit secrets, create fake decorative buttons, or claim unconfigured integrations are complete.
8. Keep project documentation current at every milestone.
