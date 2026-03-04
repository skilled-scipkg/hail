# hail source map: Simulation Workflows

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "def simulate_random_mating|def rand_|def linreg\(|def group_by\(" hail/python/hail/methods/relatedness/mating_simulation.py hail/python/hail/expr/functions.py hail/python/hail/expr/aggregators/aggregators.py`
- `rg -n "def new_job|def run\(|def declare_resource_group|def command|def cpu|def memory" hail/python/hailtop/batch/batch.py hail/python/hailtop/batch/job.py`
- `rg -n "def run_gwas|def gwas\(|def clump\(|def merge\(|def random_forest" hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py hail/python/hailtop/batch/docs/cookbook/files/run_rf_simple.py`

## Source entry points
- `hail/python/hail/methods/relatedness/mating_simulation.py` | symbol: `simulate_random_mating`
- `hail/python/hail/expr/functions.py` | symbols: `rand_int32`, `rand_norm`, `rand_beta`, `query_table`
- `hail/python/hail/expr/aggregators/aggregators.py` | symbols: `linreg`, `group_by`, `approx_quantiles`, `count`
- `hail/python/hailtop/batch/batch.py` | symbols: `Batch.new_job`, `Batch.read_input`, `Batch.write_output`, `Batch.run`
- `hail/python/hailtop/batch/job.py` | symbols: `BashJob.command`, `BashJob.declare_resource_group`, `BashJob.cpu`, `BashJob.memory`, `BashJob.image`
- `hail/python/hailtop/batch/backend.py` | symbols: `ServiceBackend._async_run`, `ServiceBackend._async_close`
- `hail/python/hailtop/batch/docs/cookbook/files/run_gwas.py` | symbol: `run_gwas`
- `hail/python/hailtop/batch/docs/cookbook/files/batch_clumping.py` | symbols: `gwas`, `clump`, `merge`
- `hail/python/hailtop/batch/docs/cookbook/files/run_rf_simple.py` | symbols: `random_forest`, `main`
- `batch/batch/driver/job.py` | symbols: `schedule_job`, `mark_job_started`, `mark_job_complete`
- `batch/batch/driver/instance_collection/job_private.py` | symbols: `compute_fair_share`, `create_instance`, `schedule_jobs_loop_body`

## Function-level behavior checks
1. Validate simulation semantics (generation/randomness) in `simulate_random_mating` and random expression functions.
2. Validate DAG/resource behavior in Batch methods before tuning cores/memory.
3. Validate service scheduler behavior in driver-side job lifecycle functions for scale issues.

## Validation checkpoints
- Simulation outputs are tied to generation/randomness code paths.
- Batch resource and dependency behavior is tied to `Batch` and `BashJob` methods.
- Scheduler claims are tied to driver lifecycle functions.
