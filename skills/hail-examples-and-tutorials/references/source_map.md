# hail source map: Examples and Tutorials

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "def run_gwas|def gwas\(|def clump\(|def merge\(" hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py`
- `rg -n "def random_forest|def checkpoint_path|def main\(" hail/python/hailtop/batch/docs/cookbook/files/run_rf_simple.py hail/python/hailtop/batch/docs/cookbook/files/run_rf_checkpoint.py hail/python/hailtop/batch/docs/cookbook/files/run_rf_checkpoint_batching.py`
- `rg -n "def run\(|def new_job|def declare_resource_group|def command" hail/python/hailtop/batch/batch.py hail/python/hailtop/batch/job.py`

## Source entry points
- `hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py` | symbols: `run_gwas`
- `hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py` | symbols: `gwas`, `clump`, `merge`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_simple.py` | symbols: `random_forest`, `main`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_checkpoint.py` | symbols: `checkpoint_path`, `random_forest`, `main`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_checkpoint_batching.py` | symbols: `checkpoint_path`, `random_forest`, `main`
- `hail/python/hailtop/batch/batch.py` | symbols: `Batch.new_job`, `Batch.read_input`, `Batch.write_output`, `Batch.run`
- `hail/python/hailtop/batch/job.py` | symbols: `BashJob.declare_resource_group`, `BashJob.command`, `BashJob.image`
- `hail/python/hailtop/tls.py` | symbols: `internal_server_ssl_context`, `internal_client_ssl_context`, `external_client_ssl_context`

## Function-level behavior checks
1. Validate cookbook assumptions by inspecting the exact script function first.
2. Validate resource-group and command wiring through `Batch` and `BashJob` methods.
3. Validate TLS recipe behavior with concrete context-construction functions.

## Validation checkpoints
- Example commands map to script entry functions in this file.
- Output contracts (`.assoc`, resource groups, merged outputs) are confirmed in code.
