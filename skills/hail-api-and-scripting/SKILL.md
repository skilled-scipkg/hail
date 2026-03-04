---
name: hail-api-and-scripting
description: This skill should be used for Hail Query Python API usage, Table/MatrixTable workflows, and hailtop Batch scripting (local and service backends).
---

# hail: API and Scripting

## High-Signal Playbook
### Route conditions
- Use this skill for Hail Query API usage (`Table`, `MatrixTable`, expressions, aggregators) and `hailtop.batch` scripting.
- Route to `hail-getting-started` if installation or first-run setup is the blocker.
- Route to `hail-troubleshooting` for auth/cloud/runtime failures.
- Route to `hail-examples-and-tutorials` for long cookbook-style workflows.

### Triage questions
- Is the workload table-centric, matrix-centric, or batch-orchestration-centric?
- Is backend Spark (`hl.init()`) or Batch (`hl.init(backend='batch')`)?
- Does batch execution need local backend or service backend?
- Are inputs local files or cloud URIs (`gs://`, `s3://`, `https://`)?
- Is confusion about documented semantics or implementation behavior?

### Canonical workflow
1. Start with API overviews:
   - `hail/python/hail/docs/api.rst`
   - `hail/python/hail/docs/overview/table.rst`
   - `hail/python/hail/docs/overview/matrix_table.rst`
   - `hail/python/hail/docs/overview/expressions.rst`
2. Prototype on tiny data (`hl.utils.range_table`, `hl.utils.range_matrix_table`) and inspect schema with `describe()`.
3. For Batch scripts, model DAG with `Batch`, `new_job` or `new_python_job`, `read_input`, `write_output`:
   - `hail/python/hailtop/batch/docs/tutorial.rst`
   - `hail/python/hailtop/batch/docs/api.rst`
4. Choose backend intentionally:
   - local iteration: `hail/python/hailtop/batch/docs/getting_started.rst`
   - service execution: `hail/python/hailtop/batch/docs/service.rst`
5. Validate output shapes and resource settings, then close service backend.
6. Escalate to source only for ambiguous behavior.

### Minimal working examples
```python
import hail as hl

hl.init()
ht = hl.utils.range_table(10)
ht = ht.annotate(bucket=ht.idx % 3)
summary = ht.group_by(ht.bucket).aggregate(n=hl.agg.count())
summary.show()
```

```python
import hailtop.batch as hb

backend = hb.ServiceBackend()
b = hb.Batch(backend=backend, name='api-smoke')
j = b.new_job(name='echo')
j.command('echo "hello world"')
b.run(open=False)
backend.close()
```

### Pitfalls and fixes
- Using Python `and` or `or` with expressions: use `&` and `|` with parentheses. See `hail/python/hail/docs/overview/expressions.rst`.
- Calling `mt.entries()` too early on large data: prefer row/col transforms first. See `hail/python/hail/docs/overview/matrix_table.rst`.
- Query-on-Batch assumptions: check beta limits in `hail/python/hail/docs/cloud/query_on_batch.rst`.
- Service backend resource leaks: always `backend.close()`.
- Clumping/GWAS jobs failing downstream output contracts: use resource groups, see `hail/python/hailtop/batch/docs/cookbook/clumping.rst`.

### Convergence and validation checks
- `describe()`, `show()`, `count`, and `count_rows` match expected schema and cardinality progression.
- Expressions are spot-checked with `hl.eval(...)` on tiny literals.
- Batch DAG passes a tiny smoke run before scaling.
- Service backend run produces outputs at the intended cloud destination.

## Primary documentation references
- `hail/python/hail/docs/api.rst`
- `hail/python/hail/docs/overview/table.rst`
- `hail/python/hail/docs/overview/matrix_table.rst`
- `hail/python/hail/docs/overview/expressions.rst`
- `hail/python/hail/docs/methods/index.rst`
- `hail/python/hail/docs/functions/index.rst`
- `hail/python/hail/docs/cloud/query_on_batch.rst`
- `hail/python/hailtop/batch/docs/getting_started.rst`
- `hail/python/hailtop/batch/docs/tutorial.rst`
- `hail/python/hailtop/batch/docs/api.rst`
- `hail/python/hailtop/batch/docs/service.rst`
- `hail/python/hailtop/batch/docs/cookbook/clumping.rst`
- `hail/python/hailtop/batch/docs/cookbook/random_forest.rst`

## Source-code entry links (when docs are insufficient)
- `hail/python/hail/table.py`
- `hail/python/hail/matrixtable.py`
- `hail/python/hail/expr/functions.py`
- `hail/python/hail/expr/aggregators/aggregators.py`
- `hail/python/hail/backend/service_backend.py`
- `hail/python/hail/backend/spark_backend.py`
- `hail/python/hailtop/batch/batch.py`
- `hail/python/hailtop/batch/job.py`
- `hail/python/hailtop/batch/backend.py`
- `batch/batch/front_end/query/query_v2.py`
- `batch/jvm-entryway/src/is/hail/JVMEntryway.java`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
