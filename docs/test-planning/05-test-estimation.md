# Test Estimation — Toolshop Test Automation

| Field | Value |
|-------|-------|
| Document ID | QA-EST-001 |
| Version | 1.1 (approved): re-estimated for a 5-week delivery by 1 engineer |
| Date | 2026-10-25 |
| Inputs | [RTM](03-requirements-traceability-matrix.md) (80 test cases), [Test Strategy](02-test-strategy.md), [Risk Register](04-risk-register.md) |

## 1. Summary

| | Value |
|---|---|
| Team | **1 QA Automation Engineer** |
| Duration | **5 weeks** (2026-10-26 → 2026-11-27) + planning week (done) |
| Effort | **137 h** remaining work + **26 h** planning (done) = **163 h** |
| Capacity | 32 h/week × 5 weeks = **160 h** |
| Buffer | **23 h (14%)**, at least 11% in every week |
| Cost | **≈ $4,075** (163 h × $25/h, assumed rate) |
| Scope | All 80 test cases written and synced to Testomat.io; all 80 automated |

## 2. Method

1. **Bottom-up estimate per task.** Work is split into epics and tasks (see the
   [Test Plan](01-test-plan.md#9-schedule-and-milestones)). Each task is estimated from the number
   of test cases it contains (API / UI / E2E counts from the RTM) and rounded to whole hours.
2. **Capacity:** 6.5 productive hours per day, rounded down to **32 h per week**. Meetings, email
   and context switching are outside this number.
3. **Buffer:** at least **11% of capacity is left free in every week**. Communication with the PO
   and unplanned work come out of the buffer.
4. **Baseline comparison:** the first estimate (v1.0, three-point PERT, 287 h) is kept in §7 so
   that the changes stay visible.

## 3. Estimate by week

### Week 1 (Oct 26 – 30): E0, E1, E2. Capacity 32 h

| Task | Test cases | Hours |
|------|-----------:|------:|
| E0. Test Planning | — | done (26 h, Oct 19 – 24) |
| E1. Test Management Setup: Testomat.io project, secrets, `.test.md` template, sync scripts, first 2 real test cases (TC-AUTH-007 UI, TC-AUTH-008 API) | 2 | 4 |
| E2-T1. Test cases: Authentication & Account | 18 | 6 |
| E2-T2. Test cases: Cart, Checkout & Orders | 20 | 6 |
| E2-T3. Test cases: Catalog & Product pages | 19 | 6 |
| E2-T4. Test cases: Admin, Contact & Non-functional | 21 | 6 |
| **Total** | **80** | **28**, buffer **4 (13%)** |

### Weeks 2–4 (Nov 2 – 20): E3, E4. Capacity 96 h

| Task | API / UI / E2E | Hours |
|------|---------------|------:|
| E3-1. First UI + first API test (TC-AUTH-007, TC-AUTH-008); the structure and config they need; regression workflow in GitHub Actions; Testomat.io reporting; P1 required for merge | 1 / 1 / 0 | 13 |
| E3-2. P1: Authentication & Account | 4 / 2 / 0 | 5 |
| E3-3. P1: Cart, Checkout & Orders | 6 / 3 / 2 | 13 |
| E3-4. P1: Catalog + Admin write-protection | 3 / 2 / 0 | 4 |
| E4-1. Regression: Authentication & Account | 9 / 3 / 0 | 9 |
| E4-2. Regression: Cart, Checkout & Orders | 5 / 4 / 0 | 8 |
| E4-3. Regression: Catalog & Product pages | 8 / 7 / 0 | 14 |
| E4-4. Regression: Admin & Contact | 8 / 5 / 1 | 14 |
| Failure triage and defect reports | — | 5 |
| **Total** | **44 / 27 / 3 = 74** | **85**, buffer **11 (11.5%)** |

### Week 5 (Nov 23 – 27): E5, E6. Capacity 32 h

| Task | Hours |
|------|------:|
| E5-1. Non-functional test cases (6): contract, response time, accessibility, cross-browser, mobile, sensitive data | 6 |
| E5-2. Stabilization: flaky tests | 8 |
| E5-3. Nightly workflow with cross-browser smoke | 3 |
| E5-4. `with-bugs` run and defect-detection metric | 2 |
| E6. Test Summary Report, README update, demo | 5 |
| **Total** | **24**, buffer **8 (25%)** |

### Totals

| | Hours |
|---|------:|
| Work, weeks 1–5 | 137 |
| Capacity, weeks 1–5 | 160 |
| **Buffer** | **23 (14%)** |
| Planning (E0, done) | 26 |
| **Whole project** | **163** |

Cross-check against the RTM: 80 test cases = 2 (E1) + 78 (E2). 74 functional cases are automated
in E3/E4 and 6 non-functional in E5. Level split 44 + 3 NFR = 47 API, 27 + 3 NFR = 30 UI, 3 E2E,
which matches the RTM.

## 4. Why the estimate is lower than the v1.0 baseline

| Factor | Effect | Evidence |
|--------|--------|----------|
| Test case design is mostly done in the RTM | Writing a case = expanding an existing RTM row (summary + expected result) into preconditions and steps | RTM rows already describe each case |
| Framework built only on demand (YAGNI) | 13 h instead of 37 h: only what the first two tests need, growing with each new test | Workflow and Testomat.io reporter already exist in the repository |
| Cloudflare workaround already found | No separate spike; the check is part of the first CI run | Verified during planning: a regular browser user agent passes the challenge |
| `data-test` attributes on the site | Little time spent on selectors in UI tests | Verified during planning (e.g. `data-test="product-name"`) |
| Published OpenAPI spec | API tests do not need endpoint discovery; many cases are data-driven variants of the same endpoint | Toolshop API v5.0.0 spec |
| Solo project | No team coordination overhead; PO communication comes out of the buffer | — |

The per-test rates behind the task hours sit between the optimistic and the most likely values of
the v1.0 PERT estimate. **This is an estimate without a P90 reserve.** It is tracked as risk
**R-12** with an explicit scope-cut rule (see §6).

## 5. Cost

Rates are **assumptions** and should be replaced with the actual contract rate.

| Item | Basis | Cost |
|------|-------|-----:|
| QA Automation Engineer | 163 h × **$25/h (assumed)** | $4,075 |
| Same, if the full buffer is used | (160 + 26) h × $25/h | $4,650 |
| GitHub Actions | Public repo: free | $0 |
| Testomat.io | Free plan for a single project (check current plan limits) | $0 |
| Playwright, axe-core, Node.js | Open source | $0 |
| **Total** | | **≈ $4,075 – $4,650** |

## 6. Assumptions and control points

**Assumptions**
- The test environment is reachable from GitHub Actions with the user-agent workaround (R-02).
- The PO answers open questions within 2 working days. Until then, expected results describe
  current behaviour.
- No major UI redesign during the project.
- Defect fixing is outside QA effort (the application is third-party).
- Excluded: load/performance testing, penetration testing, TOTP (REQ-AUTH-11), visual regression.

**Control points**
- **After the first 10 UI tests:** compare actual hours with the plan. If the deviation is over
  30%, re-estimate the remaining tasks.
- **End of week 3 (Nov 13):** if fewer than **60% of the 74 functional cases** are automated, P3
  cases move to the release-2 backlog. They stay in Testomat.io as manual test cases (R-12).

## 7. Baseline: estimate v1.0 (2026-10-24)

The first estimate used a WBS with three-point (PERT) estimates per activity and +10% management
overhead:

| | v1.0 baseline | v1.1 (current) |
|---|---:|---:|
| Effort | 287 h (P50), 319 h (P90) | 163 h |
| Duration, 1 engineer | 9–10 weeks | 5 weeks + planning week |
| Framework | 37 h, built upfront | 13 h, built on demand |
| Test case design | inside the per-test rate | separate epic, 24 h |
| Overhead | +10% | inside the weekly buffer |
| Cost | $7,175 – $7,975 | $4,075 – $4,650 |

v1.1 was produced after the decision to deliver in 5 weeks with one engineer. The scope did not
change, and the reductions are justified in §4.
