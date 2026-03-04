---
name: hail-examples-and-tutorials
description: This skill should be used when users ask for runnable Hail tutorials, cookbook patterns, or end-to-end example workflows; prioritize docs and cookbook scripts before deep source inspection.
---

# hail: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill for runnable examples, notebook-style walkthroughs, and cookbook patterns.
- Route to `hail-getting-started` if base install/config is not complete.
- Route to `hail-api-and-scripting` for API semantics without a tutorial focus.
- Route to `hail-simulation-workflows` for simulation pipeline design and scaling strategy.

### Triage questions
- Is the user asking for notebook examples, batch cookbook examples, or service-operation recipes?
- Do they need local-only runnable code or cloud Batch execution?
- Which inputs are available (VCF/MT/phenotype tables/cloud buckets)?

### Canonical workflow
1. Pick one concrete tutorial/cookbook and run it unmodified first.
2. Capture required inputs and output paths before code edits.
3. Run a minimal smoke version (small data, one chromosome, one model window).
4. Validate output shape and destination paths.
5. Only then adapt parameters/images/resources.

### Minimal runnable commands
```bash
python hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py \
  --vcf gs://hail-tutorial/1kg.vcf.bgz \
  --phenotypes gs://hail-tutorial/1kg_annotations.txt \
  --output-file /tmp/1kg-gwas
```

```bash
python hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py
```

### Validation checkpoints
- GWAS exports `.assoc`, `.bed`, `.bim`, and `.fam` files for the chosen output root.
- Batch DAG is visible and jobs complete in expected dependency order.
- Clumping output is non-empty and has one header row after merge.

## Primary documentation references
- `hail/python/hail/docs/tutorials/01-genome-wide-association-study.ipynb`
- `hail/python/hail/docs/tutorials/03-tables.ipynb`
- `hail/python/hail/docs/tutorials/04-aggregation.ipynb`
- `hail/python/hail/docs/tutorials/07-matrixtable.ipynb`
- `hail/python/hailtop/batch/docs/tutorial.rst`
- `hail/python/hailtop/batch/docs/cookbook/clumping.rst`
- `hail/python/hailtop/batch/docs/cookbook/random_forest.rst`
- `dev-docs/google-cloud-cookbook.md`
- `dev-docs/services/tls.md`
- `dev-docs/services/tls-cookbook.md`

## Source entry points for unresolved issues
- `hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py`
- `hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_simple.py`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_checkpoint.py`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_checkpoint_batching.py`
- `hail/python/hailtop/batch/batch.py`
- `hail/python/hailtop/batch/job.py`
- `hail/python/hailtop/tls.py`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
