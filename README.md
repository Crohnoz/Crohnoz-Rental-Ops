<div align="center">

<img src="https://raw.githubusercontent.com/Crohnoz/Crohnoz/main/brand/assets/logo-horizontal-dark.svg" alt="Crohnoz Labs" width="340" />

# Crohnoz Rental Ops

### Selected Engineering Case · Rental Operations & Property Administration

**Operational rules, financial traceability and public/private separation for small-building administration.**

[![CI](https://github.com/Crohnoz/Crohnoz-Rental-Ops/actions/workflows/ci.yml/badge.svg)](https://github.com/Crohnoz/Crohnoz-Rental-Ops/actions/workflows/ci.yml)

<a href="https://github.com/Crohnoz/Crohnoz/blob/main/evidence/rental-operations.md"><img src="https://img.shields.io/badge/OPEN-ENGINEERING_CASE-A855F7?style=for-the-badge" height="34" alt="Open engineering case" /></a>
<a href="https://github.com/Crohnoz"><img src="https://img.shields.io/badge/RETURN-PROFESSIONAL_PROFILE-8B5CF6?style=for-the-badge" height="34" alt="Professional profile" /></a>

**Problem → System → Evidence → Scale**

</div>

---

## Why this system exists

Small rental operations often end up split across spreadsheets, documents, receipts, chat messages and manual calculations. Crohnoz Rental Ops explores how those tasks can be turned into **explicit, traceable operational state** without forcing a heavyweight property-management stack onto a small operator.

The repository is a **sanitized public engineering surface**. Real tenant data, credentials and private deployment details are intentionally excluded.

> One private deployment currently uses the product identity **Arrendía**. This repository keeps the neutral engineering name Crohnoz Rental Ops.

---

## What it proves at a glance

| Capability | Implemented signal |
|---|---|
| **Domain modeling** | Apartments, tenants, charges, payments, contracts and exit settlements are explicit entities/workflows |
| **Financial traceability** | Rounding differences are carried forward through a recorded compensation rule |
| **Document workflow** | Vouchers, receipts, contracts and settlement outputs are part of the operation |
| **Environment separation** | Public demo mode and authenticated private mode follow different data boundaries |
| **Authorization** | Private operation uses Supabase Auth + Row Level Security |
| **Continuity** | Backup / restore and browser-local working state are part of the operating model |

This is presented as **selected operational evidence**, not as a finished multi-tenant SaaS platform.

---

## Publication architecture

### Public demonstration boundary

```env
VITE_APP_MODE=demo
```

- fictitious dataset for 23 apartments;
- mutations stay in the visitor's browser;
- demo state can be restored immediately;
- no connection to the private database.

### Private operational boundary

```env
VITE_APP_MODE=private
VITE_SUPABASE_URL=https://PROYECTO.supabase.co
VITE_SUPABASE_ANON_KEY=CLAVE_ANON_PUBLICA
```

- authenticated access with Supabase Auth;
- synchronized workspace;
- PostgreSQL / Supabase-backed state;
- Row Level Security isolates data by owner;
- temporary browser working copy in `sessionStorage`;
- real operational data is never committed to this repository or embedded in the public demo.

Detailed environment and security behavior is documented in [`docs/ENTORNOS_Y_SEGURIDAD.md`](docs/ENTORNOS_Y_SEGURIDAD.md).

---

## A concrete domain rule: rounding compensation

The calculated amount is rounded to the nearest `$100`. The difference is persisted with the opposite sign as `ajusteSiguiente`, so it can be compensated in the following charge without silently losing accounting traceability.

That rule is representative of the engineering approach used here: **business behavior is modeled explicitly instead of being hidden inside presentation code**.

---

## Quality gate

CI validates both publication modes rather than assuming that one successful build proves both contexts:

```text
validate demo seed
→ validate environment routing
→ build demo
→ build private shell
→ validate Arrendía theme bundle
```

This guards the separation between public demonstration and private operation and catches visual/routing changes that could silently break one mode.

---

## Current engineering surface

`React` · `Vite` · `JavaScript` · `Supabase Auth` · `PostgreSQL / Supabase` · `RLS` · `Netlify`

<details>
<summary><strong>Local development</strong></summary>

<br/>

```bash
cp .env.example .env
npm install
npm run dev
```

Production build:

```bash
npm run build
```

</details>

---

## Current boundaries

The current private implementation uses one owner per workspace. Moving toward a broader multi-user product would require explicit organizations, memberships, roles, user-level auditability and additional domain normalization.

The public repository therefore does **not** claim multi-tenant SaaS maturity. Its value is the inspectable engineering around operational rules, finance, environment isolation, authorization and continuity.

---

<div align="center">

### Crohnoz Labs

**Evidence is public by design. Product implementation is private by default.**

<a href="https://github.com/Crohnoz/Crohnoz/blob/main/evidence/rental-operations.md"><img src="https://img.shields.io/badge/REVIEW-CURATED_CASE-A855F7?style=for-the-badge" height="34" alt="Review curated case" /></a>
<a href="https://crohnozlabs.cl"><img src="https://img.shields.io/badge/ENTER-CROHNOZ_LABS-EC4899?style=for-the-badge" height="34" alt="Crohnoz Labs" /></a>

</div>
