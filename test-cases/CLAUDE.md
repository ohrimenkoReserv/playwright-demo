# Writing test cases

Rules for creating and editing `*.test.md` files in this folder. The full format, with the
template and an example, is in [README.md](README.md). Read it before writing a case. The
Testomat.io format reference is
[Classical Tests Markdown Format](https://docs.testomat.io/project/import-export/export-tests/classical-tests-markdown-format/).

## Before writing

- Take the case from its RTM row
  ([03-requirements-traceability-matrix.md](../docs/test-planning/03-requirements-traceability-matrix.md)):
  TC ID, requirement, priority, level, smoke flag. Do not invent cases that are not in the RTM.
  The TC ID and the requirement go into the tags.
- Do not write expected results from memory. Check them against the product: the OpenAPI spec
  (`https://api.practicesoftwaretesting.com/docs?api-docs.json`) for API cases, the Toolshop UI
  source or the live UI for UI cases. Name the source in the issue notes.
- Test data: each case creates its own data via the API (e.g. a new customer registered with
  `POST /users/register`). Do not rely on the shared demo accounts (risk R-01).

## File

- One case per file: `test-cases/<module>/<test-case-title>.test.md`. The file name, the suite
  heading (`# …`) and the case title (`## …`) are the same text. When the title changes,
  rename the file and change both headings.
- Every file starts with a `<!-- suite -->` block. Without it Testomat.io does not create the
  case. The suite is technical and must stay unique, so never reuse a suite name in another file.
- Do not group cases by suite. Grouping is by module folder and by tags only.

## Metadata

```markdown
<!-- test
priority: critical
tags: TC-AUTH-007, ui, auth, REQ-AUTH-05, regression, smoke
-->
```

- `priority` is a field, never a tag: P1 → `critical`, P2 → `normal`, P3 → `low`. Do not use
  `high` or `important`.
- `tags`, in this order: TC ID (`TC-*`, the RTM row), level (`ui` / `api` / `e2e`), module
  (the folder name, e.g. `auth`), requirement (`REQ-*`, as in the RTM row), `regression` (every
  case), then `smoke` if the RTM marks the case as smoke. Comma-separated, without `@`.
- Never add, edit or remove `id: @S…` / `id: @T…` by hand, except to restore IDs that
  `tms:push` failed to write (see the Windows issue in README). New cases have no `id`.
- Testomat IDs live only in the case files. Do not copy them into `docs/test-planning/` (RTM,
  strategy, plan): the RTM links to a case through its `TC-*` and `REQ-*` tags.

## Body

```markdown
## Preconditions

- <state of the system and test data before step 1, and how it is prepared>

## Steps

1. <one user action or one request>
*Expected*: <observable result of this step>
2. <action without its own checkable result>
3. <action>
*Expected*: <observable result>
```

- Use `## Preconditions` and `## Steps` headings. Do not use bold labels (`**Steps**`) and do
  not add a separate `## Expected result` section: Testomat.io attaches only `*Expected*:` lines
  inside `## Steps` to their step.
- Each `*Expected*:` is one line directly under its step, never wrapped. Put several results of
  one step in one sentence.
- A step that has no checkable result of its own (e.g. typing into a field) has no
  `*Expected*:` line.
- Expected results describe only what the user sees or what the API returns, and can be judged
  pass or fail. No selectors, code or implementation details.
- Write in English. The title describes the behaviour being checked, without tags or IDs.

## Checking and syncing

- Check that the file parses, without sending anything:
  `env -u TESTOMATIO TESTOMATIO= npx check-tests push -d test-cases`. Expect one suite and one
  case per file, with the right tags.
- `npm run tms:push` writes to the Testomat.io project. Run it only when the user asks.
- After a push, check `id: @S…` and `id: @T…` in the file. On Windows the IDs are not written
  back into the file (`0 files updated`), see README.
- If the push fails with `422: Pull latest changes`, do not add `--force` on your own. Tell the
  user and follow README.
- After a push, check the case in Testomat.io: priority, tags, steps with Expected, and that
  Out of sync is empty.
- When the format or rules change, update README.md, this file and
  [Test Strategy §8](../docs/test-planning/02-test-strategy.md#8-test-management-testomatio)
  together.
