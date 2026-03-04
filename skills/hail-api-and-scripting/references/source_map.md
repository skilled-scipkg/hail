# hail source map: API and Scripting

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "class Table|class MatrixTable|def rand_|def group_by\(|def query_table" hail/python/hail/table.py hail/python/hail/matrixtable.py hail/python/hail/expr/functions.py`
- `rg -n "def count\(|def linreg\(|def approx_quantiles\(|def group_by\(" hail/python/hail/expr/aggregators/aggregators.py`
- `rg -n "def new_job|def new_python_job|def read_input|def write_output|def run\(" hail/python/hailtop/batch/batch.py`
- `rg -n "def declare_resource_group|def command|def cpu|def memory|def image" hail/python/hailtop/batch/job.py`

## Source entry points
- `hail/python/hail/table.py` | symbols: `Table`, `Table.annotate`, `Table.group_by`, `Table.filter`
- `hail/python/hail/matrixtable.py` | symbols: `MatrixTable`, `MatrixTable.annotate_rows`, `MatrixTable.filter_rows`
- `hail/python/hail/expr/functions.py` | symbols: `rand_int32`, `rand_norm`, `group_by`, `query_table`
- `hail/python/hail/expr/aggregators/aggregators.py` | symbols: `count`, `group_by`, `linreg`, `approx_quantiles`
- `hail/python/hail/backend/service_backend.py` | symbols: `ServiceBackend._rpc`, `ServiceBackend.validate_file`, `ServiceBackend.stop`
- `hail/python/hail/backend/spark_backend.py` | symbols: `SparkBackend`
- `hail/python/hailtop/batch/batch.py` | symbols: `Batch.new_job`, `Batch.new_python_job`, `Batch.read_input`, `Batch.write_output`, `Batch.run`
- `hail/python/hailtop/batch/job.py` | symbols: `BashJob.declare_resource_group`, `BashJob.command`, `BashJob.cpu`, `BashJob.memory`
- `hail/python/hailtop/batch/backend.py` | symbols: `LocalBackend`, `ServiceBackend`, `Backend.close`
- `batch/batch/front_end/query/query_v2.py` | symbols: `parse_list_batches_query_v2`, `parse_job_group_jobs_query_v2`
- `batch/jvm-entryway/src/is/hail/JVMEntryway.java` | symbols: `main`, `finishException`

## Function-level behavior checks
1. Confirm API semantics in `hail/python/hail/table.py` or `hail/python/hail/matrixtable.py` before attributing behavior to docs.
2. Confirm expression and aggregation semantics in `hail/python/hail/expr/functions.py` and `hail/python/hail/expr/aggregators/aggregators.py` for edge cases.
3. Confirm Batch orchestration semantics (`Batch.run`, `BashJob.command`, resource declarations) before diagnosing DAG behavior.

## Validation checkpoints
- Every API behavior claim maps to at least one source symbol above.
- Backend-specific claims are validated in both Spark and service backend code paths when relevant.
