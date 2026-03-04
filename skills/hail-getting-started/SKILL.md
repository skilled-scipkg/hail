---
name: hail-getting-started
description: This skill should be used for first-run Hail setup, install/runtime prerequisites, first analysis, and tutorial notebook entry points.
---

# hail: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill for first-time setup, first runnable query, backend selection, and tutorial starting points.
- Route to `hail-build-and-install` for contributor/source builds.
- Route to `hail-api-and-scripting` for deeper API semantics after first run succeeds.
- Route to `hail-troubleshooting` for auth/cloud/runtime failures.

### Triage questions
- Platform: macOS, Linux, Dataproc, or another Spark cluster?
- Backend target: Spark or Query-on-Batch?
- Are Java 11 and Python 3.10+ available?
- For Batch backend, are auth, billing project, and remote tmpdir configured?
- Does user want script-first flow or notebook-first flow?

### Canonical workflow
1. Pick install track:
   - local: `hail/python/hail/docs/install/linux.rst` or `hail/python/hail/docs/install/macosx.rst`
   - cloud: `hail/python/hail/docs/install/dataproc.rst` or `hail/python/hail/docs/cloud/query_on_batch.rst`
2. Confirm prerequisites before `pip install hail`.
3. Run first query from `hail/python/hail/docs/install/try.rst`.
4. Introduce data model from:
   - `hail/python/hail/docs/overview/table.rst`
   - `hail/python/hail/docs/overview/matrix_table.rst`
   - `hail/python/hail/docs/overview/expressions.rst`
5. For Batch backend, configure `batch/billing_project`, `batch/remote_tmpdir`, and `query/backend=batch`.
6. Route into tutorials after first query succeeds.

### Minimal working examples
```python
import hail as hl

hl.init()
mt = hl.balding_nichols_model(n_populations=3, n_samples=10, n_variants=100)
mt.show()
print(mt.count())
```

```python
import hailtop.batch as hb

b = hb.Batch()
j = b.new_job(name='hello')
j.command('echo "hello world"')
b.run()
```

### Pitfalls and fixes
- Apple silicon Java mismatch: install arm64 Java 11.
- macOS binary build errors: use `pip install hail --only-binary=:all:`.
- Dataproc setup fails early: configure `gcloud` project and region first.
- Query-on-Batch fails without Hail auth and config keys: run `hailctl auth login` and set required config.

### Convergence and validation checks
- `import hail as hl; hl.init(); print(hl.version())` succeeds.
- First query from `hail/python/hail/docs/install/try.rst` runs.
- `hl.current_backend()` matches expected backend.
- For Batch backend, `hailctl config list` shows billing project, remote tmpdir, and backend.
- One tutorial notebook opens and first cells execute.

## Primary documentation references
- `hail/python/hail/docs/getting_started.rst`
- `hail/python/hail/docs/install/linux.rst`
- `hail/python/hail/docs/install/macosx.rst`
- `hail/python/hail/docs/install/dataproc.rst`
- `hail/python/hail/docs/install/try.rst`
- `hail/python/hail/docs/overview/table.rst`
- `hail/python/hail/docs/overview/matrix_table.rst`
- `hail/python/hail/docs/overview/expressions.rst`
- `hail/python/hail/docs/cloud/query_on_batch.rst`
- `hail/python/hailtop/batch/docs/getting_started.rst`
- `hail/python/hailtop/batch/docs/tutorial.rst`

## Tutorial notebook entry points
- `hail/python/hail/docs/tutorials/01-genome-wide-association-study.ipynb`
- `hail/python/hail/docs/tutorials/03-tables.ipynb`
- `hail/python/hail/docs/tutorials/04-aggregation.ipynb`
- `hail/python/hail/docs/tutorials/07-matrixtable.ipynb`

## Source-code entry links (when docs are insufficient)
- `hail/python/hail/context.py`
- `hail/python/hail/backend/spark_backend.py`
- `hail/python/hail/backend/service_backend.py`
- `hail/python/hailtop/batch/batch.py`
- `hail/python/hailtop/batch/backend.py`
- `hail/python/hailtop/hailctl/auth/login.py`
- `hail/python/hailtop/hailctl/batch/initialize.py`
- `hail/python/test/hail/test_context.py`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
