# Test Planning — Toolshop (practicesoftwaretesting.com)

Phase 1 of the automation initiative: **planning before code**.

The product is the *Toolshop* web store (Angular SPA + Laravel REST API, OpenAPI v5.0.0) at
<https://practicesoftwaretesting.com>. At the start of this initiative it has **no automated tests,
no written requirements and no test documentation** — only the running application and the
published Swagger spec. All requirements below were reverse-engineered from exploratory sessions
and the API spec, and are listed as *baseline requirements to be confirmed with the Product Owner*.

## Artifacts

| # | Artifact | Purpose | Status |
|---|----------|---------|--------|
| 1 | [Test Plan](01-test-plan.md) | Scope, schedule, roles, entry/exit criteria, resources | Approved v1.1 |
| 2 | [Test Strategy](02-test-strategy.md) | Standards, test levels and types, tooling, conventions | Approved v1.1 |
| 3 | [Requirements Traceability Matrix](03-requirements-traceability-matrix.md) | Requirements → test cases → automation | Approved v1.0 |
| 4 | [Risk Register](04-risk-register.md) | Product and project risks with mitigation | Approved v1.1 |
| 5 | [Test Estimation](05-test-estimation.md) | Effort, people, cost | Approved v1.1 |

## How the artifacts connect

```
Exploratory session + OpenAPI spec
        │
        ▼
Baseline requirements (REQ-*) ──► Risk Register (R-*) ──► priority of each REQ
        │                                                     │
        ▼                                                     ▼
RTM: REQ-* → TC-* (level, priority) ──────────────► Test Estimation (effort per TC)
        │                                                     │
        ▼                                                     ▼
Test Plan (what / when / who / done) + Test Strategy (how) ◄──┘
        │
        ▼
TC-* written as plain-language cases in test-cases/*.test.md ──► synced to Testomat.io (IDs)
        │
        ▼
Automated Playwright tests carry the case's Testomat ID ──► CI results land on the same case
```

## Discovery facts that shaped the plan

Observed on 2026-10-24 during the initial exploratory session:

- API: ~90 operations across 17 resources (products, carts, invoices, payments, users, admin, reports…).
- Catalog: 50 products, 9 per page, 3 top-level categories / 16 subcategories.
- Checkout supports 5 payment methods: bank transfer, cash on delivery, credit card, buy now pay later, gift card.
- Password policy: ≥ 8 chars, upper + lower case, digit, symbol (confirmed via API validation).
- The shared demo account `customer@practicesoftwaretesting.com` was **locked** ("too many failed
  attempts") by other users of the public environment → tests must own their test data (see R-01).
- The UI is behind a **Cloudflare challenge** (non-browser clients get HTTP 403) → CI runners may be
  challenged (see R-02).
- Seed data has today's `created_at` → the database is **reset periodically** (see R-04).
- A fault-seeded variant of the API exists (`api-with-bugs.practicesoftwaretesting.com`) — used to
  verify that the suite actually detects defects (mutation-style check of test effectiveness).
