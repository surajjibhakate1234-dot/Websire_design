# EMBER & OAK — System Architecture

**Version:** 1.0 (Phase 0 Baseline)  
**Architecture Style:** Modular Monolith (Next.js App Router + Supabase)

---

## 1. Architectural Principles

1. **Commerce First:** Navigation, menu browsing, product customization, cart, checkout, order tracking, and reservations must function completely without WebGL or 3D assets.
2. **Strict Layer Separation:**
   - **UI Components (`src/components/`, `src/app/`)**: Presentation and user interaction only.
   - **3D Presentation Layer (`src/components/3d/`)**: Strictly presentation & navigation triggers; zero pricing, order, auth, or database logic.
   - **Server Services (`src/server/services/`)**: All business rules, pricing math, order state transitions, reservation availability, inventory ledger mutations, and RBAC enforcement.
   - **Repositories (`src/server/repositories/`)**: Typed PostgreSQL / Supabase queries.
   - **External Providers (`src/server/providers/`)**: Swappable interfaces for payments, delivery, and notifications.
3. **Server-Side Authority:** Never trust client-submitted prices, discounts, tax amounts, role claims, or frontend payment redirects.
4. **Single Deployable Monolith:** Avoid microservices or a second backend framework (e.g., NestJS) unless a documented technical constraint requires it.

---

## 2. Technology Stack

| Layer | Choice | Purpose |
|---|---|---|
| Framework | Next.js (App Router) | SSR/RSC storefront, admin routes, API route handlers |
| UI & Styling | React, TypeScript (strict), Tailwind CSS | Editorial design system & responsive layouts |
| 3D Graphics | Three.js, React Three Fiber, Drei, GSAP | Lazy-loaded, progressive 3D café hero & guided camera |
| Database | PostgreSQL (Supabase) | Relational schema, transactions, Row Level Security |
| Auth & Storage | Supabase Auth & Supabase Storage | Staff/customer auth and product/gallery media storage |
| Validation | Zod | Request, form, and environment schema validation |
| Client State | Zustand | Cart drawer, UI/3D view state (non-authoritative) |
| Testing | Vitest & Playwright | Unit, integration, and end-to-end verification |
| Hosting | Vercel + Supabase | Edge/serverless app hosting + managed Postgres |

---

## 3. Data & Domain Invariants

- **Currency (INR):** Every monetary value is stored and computed in **integer paise** (`₹150.00 = 15000`). Floating-point rupees are never used in calculations or database columns.
- **Timestamps & Timezones:** Stored in **UTC** (`timestamptz`) in PostgreSQL; converted to the café's configured timezone (`Asia/Kolkata` / IST) for business-hour checks, reservation slots, and UI display.
- **Immutable Financial & Historical Records:**
  - `order_items` capture snapshot product names, variant names, modifier snapshots, and unit/line prices at purchase time.
  - Products referenced by past orders are archived (`archived_at`), never hard-deleted.
  - Order transitions append to `order_status_history`; admin actions append to `audit_logs`.
  - Inventory (`stock_movements`) and loyalty (`loyalty_transactions`) use append-only ledgers rather than direct balance overwrites.

---

## 4. Security & Authorization Model

### Roles (`staff_roles` / `staff_memberships`)
- `owner` — Full access across catalog, orders, reservations, inventory, delivery, staff, analytics, settings.
- `manager` — Daily operations, menu, orders, reservations, inventory, delivery, promotions.
- `staff` — Authorized order handling, reservation check-in, customer assistance.
- `kitchen` — Preparation queue and `accepted → preparing → ready` transitions.
- `delivery` — Assigned deliveries and delivery status updates.
- `customer` — Own profile, addresses, orders, and reservations only.

### Defense-in-Depth Controls
- **PostgreSQL RLS:** Enabled on every table containing business or customer data.
- **Server Guards:** Every `/api/v1/admin/*`, `/admin`, `/kitchen`, and `/delivery` entry point verifies authenticated identity and required role server-side.
- **Payment Security:** Server-side payment creation, HMAC-signed webhook verification, idempotency via `payment_events`, zero storage of card PAN/CVV.
- **Secrets Hygiene:** Service-role keys and webhook secrets are server-only environment variables; never exposed in `NEXT_PUBLIC_*` or browser bundles.

---

## 5. Planned Versioned API Surface (`/api/v1`)

| Method | Endpoint | Auth | Responsibility |
|---|---|---|---|
| `GET` | `/api/v1/menu` | Public | Active categories, products, variants, modifiers, availability |
| `GET` | `/api/v1/products/:slug` | Public | Full product detail & customization schema |
| `POST` | `/api/v1/orders/quote` | Public / Customer | Authoritative server-side subtotal, tax, discount, fee calculation |
| `POST` | `/api/v1/orders` | Public / Customer | Idempotent order creation with live availability & modifier checks |
| `GET` | `/api/v1/orders/:id` | Authorized (owner/staff or order token/customer) | Order details & status timeline |
| `POST` | `/api/v1/payments/create` | Authorized | Initiate payment attempt via configured provider adapter |
| `POST` | `/api/v1/payments/webhook` | Signed Provider Callback | Verify signature, deduplicate event, finalize payment & order state |
| `GET` | `/api/v1/reservations/availability` | Public | Compute open time slots by date, party size, seating zone |
| `POST` | `/api/v1/reservations` | Public / Customer | Transactional conflict-free booking creation |
| `GET` | `/api/v1/admin/orders` | Staff / Kitchen / Manager / Owner | Paginated, filterable operational order queue |
| `PATCH` | `/api/v1/admin/orders/:id/status` | Authorized Role | Validated order state transition + audit entry |
| `CRUD` | `/api/v1/admin/products` | Manager / Owner | Product, variant, modifier & availability management |
| `CRUD` | `/api/v1/admin/reservations` | Staff / Manager / Owner | Reservation approval, seating & cancellation management |
| `GET/PATCH` | `/api/v1/admin/settings` | Owner / Manager | Business hours, tax rules, fulfilment & store metadata |

Detailed request/response Zod schemas will be documented in `docs/api-contract.md` as endpoints are implemented in Phases 2–5.
