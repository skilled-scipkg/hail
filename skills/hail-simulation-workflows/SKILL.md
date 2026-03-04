---
name: hail-simulation-workflows
description: This skill should be used for Hail simulation workflow design and execution (data simulation, batch DAG orchestration, resource sizing, and reproducibility checks) using docs-first guidance and source-level validation when needed.
---

# hail: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for simulation pipeline design, batch orchestration, and reproducibility validation.
- Route to `hail-getting-started` if environment/auth is not ready.
- Route to `hail-api-and-scripting` for API semantics outside simulation flow design.
- Route to `hail-troubleshooting` for active runtime/service failures.

### Required inputs before running
- Backend choice: local Spark vs Batch service.
- Input data source: synthetic (`hl.balding_nichols_model`) or file-backed (`vcf`, `mt`, phenotypes).
- Output location: local path or cloud URI.
- Compute envelope: cores/memory/storage per step.
- Reproducibility settings: random seed, fixed image tags, fixed input versions.

### Canonical workflow
1. Start with the smallest runnable workflow on synthetic or tutorial data.
2. Validate each stage output before adding downstream jobs.
3. Encode resources per job explicitly (`cpu`, `memory`, resource groups).
4. Move to service backend only after local smoke pass.
5. Scale dimensions (samples, variants, chromosome fan-out) gradually.

### Minimal working examples
```python
import hail as hl

hl.init()
mt = hl.balding_nichols_model(n_populations=3, n_samples=50, n_variants=500)
mt = hl.variant_qc(mt)
print(mt.count_rows(), mt.count_cols())
```

```bash
python hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py \
  --vcf gs://hail-tutorial/1kg.vcf.bgz \
  --phenotypes gs://hail-tutorial/1kg_annotations.txt \
  --output-file /tmp/1kg-gwas
```

### Validation checkpoints
- Simulation output dimensions match configured inputs.
- Randomness behavior is explicit (seed/reset strategy documented).
- Batch DAG produces expected artifacts and dependency ordering.
- Output contract is verified (expected file groups/columns/row counts).

## Primary documentation references
- `hail/python/hail/docs/guides/genetics.rst`
- `hail/python/hail/docs/cloud/query_on_batch.rst`
- `hail/python/hailtop/batch/docs/tutorial.rst`
- `hail/python/hailtop/batch/docs/service.rst`
- `hail/python/hailtop/batch/docs/cookbook/clumping.rst`
- `hail/python/hailtop/batch/docs/cookbook/random_forest.rst`
- `dev-docs/services/batch/job-container-design.md`
- `dev-docs/services/batch/design.rst`
- `hail/hail/test/resources/ldprune_corrtest.txt`

## Source entry points for unresolved issues
- `hail/python/hail/methods/relatedness/mating_simulation.py`
- `hail/python/hail/expr/functions.py`
- `hail/python/hail/expr/aggregators/aggregators.py`
- `hail/python/hailtop/batch/batch.py`
- `hail/python/hailtop/batch/job.py`
- `hail/python/hailtop/batch/backend.py`
- `hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py`
- `hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py`
- `batch/batch/driver/job.py`
- `batch/batch/driver/instance_collection/job_private.py`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
