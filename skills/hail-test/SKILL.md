---
name: hail-test
description: This skill should be used for choosing and running Hail tests (Python/JVM/QoB/inter-cloud), using fixtures correctly, and validating fixes quickly.
---

# hail: Test

## High-Signal Playbook
### Route conditions
- Use this skill for test planning/execution, regression validation, fixture usage, and flaky-test diagnosis.
- Route to `hail-troubleshooting` for active service incidents beyond test scope.
- Route to `hail-build-and-install` when failures are environment/build setup issues.

### Triage questions
- Which layer changed: Query Python, Query JVM, Batch service, hailctl, or infra tooling?
- Which backend matters: `spark`, `batch` (QoB), or `local`?
- Is this unit, integration, inter-cloud, or doctest?
- Are namespace/remote resource prerequisites satisfied?
- Are deterministic randomness guarantees required in assertions?

### Canonical workflow
1. Start with the narrowest target (`PYTEST_TARGET` file or `-k` selector).
2. Run local Python tests via `make -C hail pytest ...`.
3. Run backend-specific suites only when needed (`pytest-qob` for Batch backend).
4. Use fixture helpers and backend markers from:
   - `hail/python/test/hail/conftest.py`
   - `hail/python/test/hail/helpers.py`
5. For remote-resource tests, refresh upload prerequisites from `hail/Makefile`.
6. For flaky CI behavior, use `dev-docs/services/flaky_tests.md`.
7. Expand to broader suites only after focused pass is green.

### Minimal working examples
```bash
make -C hail install-editable
make -C hail pytest PYTEST_TARGET=test/hail/test_context.py
make -C hail pytest PYTEST_TARGET=test/hail/table/test_table.py PYTEST_ARGS='-k annotate'
```

```python
import hail as hl

hl.reset_global_randomness()
ht = hl.utils.range_table(5).annotate(x=hl.rand_int32(5))
assert ht.count() == 5
```

### Pitfalls and fixes
- QoB tests fail without namespace setup: run `make -C hail pytest-qob NAMESPACE=<ns> ...`.
- Remote fixture data expired: rerun upload targets in `hail/Makefile`.
- Unexpected skips from backend markers: inspect marker handling in `hail/python/test/hail/conftest.py`.
- Doctest rendering failures: use `doctest-query` target constraints in `hail/Makefile`.
- Flaky tests recur without signal: use DB-query runbook in `dev-docs/services/flaky_tests.md`.

### Convergence and validation checks
- One targeted smoke test passes in touched module.
- Backend-relevant path (Spark or QoB) passes for changed behavior.
- Regression reproduces before fix and no longer reproduces after fix.
- Skip/xfail behavior in touched area is unchanged unless intentionally modified.

## Primary documentation references
- `dev-docs/development-process.md`
- `dev-docs/services/flaky_tests.md`
- `hail/python/hail/docs/getting_started_developing.rst`
- `hail/Makefile`
- `hail/python/test/hail/conftest.py`
- `hail/python/test/hail/helpers.py`
- `hail/python/test/hail/test_context.py`
- `hail/python/test/hail/test_randomness.py`
- `hail/python/test/hail/table/test_table.py`
- `batch/test/test_batch.py`

## Source-code entry links (when docs are insufficient)
- `hail/Makefile`
- `hail/python/test/hail/conftest.py`
- `hail/python/test/hail/helpers.py`
- `hail/python/test/hail/test_context.py`
- `hail/python/test/hail/test_randomness.py`
- `hail/python/test/hail/table/test_table.py`
- `batch/test/test_batch.py`
- `hail/python/hail/context.py`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
