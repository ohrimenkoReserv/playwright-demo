# Test cases

Test cases for Toolshop, written in plain language so that each one can be run manually or
automated. This folder is the source of truth: cases are synced to Testomat.io from here.

- One file per product module: `<module>.test.md` (e.g. `auth.test.md`, `cart.test.md`).
- Every case comes from the [RTM](../docs/test-planning/03-requirements-traceability-matrix.md).
- Only `*.test.md` files are synced. This README is not.

## Sync with Testomat.io

Requires `TESTOMATIO` in the local `.env` (see the project README).

```bash
npm run tms:push   # send cases to Testomat.io and write their IDs back into the files
npm run tms:pull   # bring back edits made in the Testomat.io UI
```

Commit the files after `tms:push`, so the Testomat IDs are stored in the repository.

## File format

```markdown
<!-- suite
-->
# <Module name>

<!-- test
tags: <TC-ID>, <level>, <priority>, <REQ-ID>[, smoke]
-->
## <What is checked, as observable behaviour>

**Preconditions**
- <State of the system and data before the test>

**Steps**
1. <Action>
2. <Action>

**Expected result**
- <Observable result that can be checked>
```

- `# <Module name>` is the suite. `## <title>` is the test case. A case starts at its
  `<!-- test` block and ends at the next one.
- After `tms:push`, Testomat IDs appear in the blocks as `id: @S…` (suite) and `id: @T…` (case).
  Do not edit or remove them: automated tests refer to cases by these IDs.
- Add new cases without an `id`. They get one on the next `tms:push`.

## Tags

| Tag | Values | Meaning |
|-----|--------|---------|
| Test case | `TC-<AREA>-<NNN>` | Test case ID from the RTM, links the case to its RTM row |
| Level | `api`, `ui`, `e2e` | Layer the case runs on (see [Test Strategy §4](../docs/test-planning/02-test-strategy.md#4-test-levels)) |
| Priority | `P1`, `P2`, `P3` | Risk-based priority from the RTM |
| Requirement | `REQ-<AREA>-<NN>` | Requirement the case covers, as in the RTM |
| Smoke | `smoke` | Included in the smoke subset (optional) |

## Writing rules

- **Title:** the behaviour being checked, in English, e.g. "Customer logs in with valid
  credentials". Do not put tags or IDs in the title.
- **Preconditions:** everything that must be true before step 1, including test data. Say how it
  is prepared if it matters (e.g. "created via the API").
- **Steps:** one user action or one request per step, numbered. No implementation details such as
  selectors or code.
- **Expected result:** observable outcomes only (what the user sees or what the API returns).
  Each item must be checkable as pass or fail.
- **One case per RTM test case:** the `TC-*` tag must match the RTM row the case implements.

## Example

```markdown
<!-- test
tags: TC-CART-003, ui, P1, REQ-CART-02
-->
## Changing quantity recalculates line and cart totals

**Preconditions**
- Customer is logged in.
- Cart contains 1 × "Combination Pliers".

**Steps**
1. Open the cart page.
2. Change the quantity of "Combination Pliers" from 1 to 3.

**Expected result**
- Line total equals unit price × 3.
- Cart total is updated to the new line total.
```
