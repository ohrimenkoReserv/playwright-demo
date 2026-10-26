# Test cases

Test cases for Toolshop, written in plain language so that each one can be run manually or
automated. This folder is the source of truth: cases are synced to Testomat.io from here.

- One file per test case, in a folder per product module: `<module>/<test-case-title>.test.md`
  (e.g. `auth/Customer logs in with valid credentials via the login form.test.md`). The file name
  is the case title (`## <title>`) exactly; rename the file when the title changes.
- Every case comes from the [RTM](../docs/test-planning/03-requirements-traceability-matrix.md).
- Only `*.test.md` files are synced. This README is not.

## Sync with Testomat.io

Requires `TESTOMATIO` in the local `.env` (see the project README).

```bash
npm run tms:push   # send cases to Testomat.io and write their IDs back into the files
npm run tms:pull   # bring back edits made in the Testomat.io UI
```

Commit the files after `tms:push`, so the Testomat IDs are stored in the repository.

**Push rejected with `422: Pull latest changes`:** Testomat.io stores its own copy of each file
(tags in the title, `priority`, `creator`) and treats it as newer than the local one. Run
`npm run tms:pull` first and review the diff, or, when the repository version is the one to keep,
`npx check-tests push -d test-cases --force`.

**Known issue on Windows:** `check-tests` 0.22.2 sends the cases but does not write the IDs back
(`0 files updated`): it builds the file pattern with backslashes, which `glob` reads as escape
characters and matches no files (Git Bash does not help, Node still uses Windows paths). The
cases are still created in Testomat.io. Run `tms:push` from WSL, Linux or macOS, or add the
`id: @S…` / `id: @T…` lines from Testomat.io by hand.

## File format

```markdown
<!-- suite
-->
# <What is checked, as observable behaviour>

<!-- test
priority: <critical | normal | low>
tags: <TC-ID>, <level>, <module>, <REQ-ID>, regression[, smoke]
-->
## <What is checked, as observable behaviour>

## Preconditions

- <State of the system and data before the test>

## Steps

1. <Action>
*Expected*: <Observable result of this step>
2. <Action>
*Expected*: <Observable result of this step>
```

- `## <title>` after the `<!-- test` block is the test case. A file holds one case.
- The `<!-- suite` block with `# <title>` is technical: Testomat.io does not import a case that
  has no suite. Use the same text for the file name, the suite and the case title.
- In Testomat.io one file is one suite, so every case has its own suite. The module folder
  (`auth/`) becomes a Testomat.io folder that holds these suites. Testomat.io does not merge
  suites from different files, even with the same name and ID.
- Suites carry no meaning. Cases are grouped and selected only by tags: the smoke set is every
  case tagged `smoke`, the API set every case tagged `api`, and so on. CI selects automated tests
  the same way (`--grep @smoke`, see
  [Test Strategy §8](../docs/test-planning/02-test-strategy.md#8-test-management-testomatio)).
- After `tms:push`, Testomat IDs appear in the blocks as `id: @S…` (suite) and `id: @T…` (case).
  Do not edit or remove them: automated tests refer to cases by these IDs.
- Add new cases without an `id`. They get one on the next `tms:push`.
- `## Steps` is the Testomat.io steps format: a numbered list, and the `*Expected*:` line under a
  step is the expected result of that step. Keep each `*Expected*:` on one line. `## Preconditions`
  is part of the description.

## Priority

Priority is the Testomat.io `priority` field, not a tag. It maps to the RTM priority:

| RTM | `priority:` | Meaning |
|-----|--------------|---------|
| P1 | `critical` | Must pass for release, gates every merge |
| P2 | `normal` | Regression |
| P3 | `low` | Nice to have, nightly |

Testomat.io also accepts `high` and `important`; they are not used.

## Tags

| Tag | Values | Meaning |
|-----|--------|---------|
| Level | `api`, `ui`, `e2e` | Layer the case runs on (see [Test Strategy §4](../docs/test-planning/02-test-strategy.md#4-test-levels)) |
| Test case | `TC-<AREA>-<NNN>` | Test case ID from the RTM, links the case to its RTM row |
| Module | `auth`, `cart`, … | Product module, the same as the folder name |
| Requirement | `REQ-<AREA>-<NN>` | Requirement the case covers, as in the RTM |
| Regression | `regression` | Every case: part of the regression run |
| Smoke | `smoke` | Included in the smoke subset (optional) |

## Writing rules

- **Title:** the behaviour being checked, in English, e.g. "Customer logs in with valid
  credentials". Do not put tags or IDs in the title.
- **Preconditions:** everything that must be true before step 1, including test data. Say how it
  is prepared if it matters (e.g. "created via the API").
- **Steps:** one user action or one request per step, numbered. No implementation details such as
  selectors or code.
- **Expected:** observable outcomes only (what the user sees or what the API returns), under the
  step that causes them. Each one must be checkable as pass or fail. A step without a checkable
  outcome of its own (e.g. typing into a field) has no `*Expected*:` line.
- **One case per RTM test case:** the `TC-*` and `REQ-*` tags must match the RTM row the case
  implements.

## Example

File `cart/Changing quantity recalculates line and cart totals.test.md`:

```markdown
<!-- suite
-->
# Changing quantity recalculates line and cart totals

<!-- test
priority: critical
tags: TC-CART-003, ui, cart, REQ-CART-02, regression
-->
## Changing quantity recalculates line and cart totals

## Preconditions

- Customer is logged in.
- Cart contains 1 × "Combination Pliers".

## Steps

1. Open the cart page.
*Expected*: The cart shows 1 × "Combination Pliers".
2. Change the quantity of "Combination Pliers" from 1 to 3.
*Expected*: The line total equals unit price × 3, and the cart total is updated to the new line total.
```
