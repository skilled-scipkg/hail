# hail source map: Test

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "def init_hail|def init_query_on_batch|def pytest_collection_modifyitems" hail/python/test/hail/conftest.py`
- `rg -n "def hl_init_for_test|def skip_|def test_timeout|def with_flags" hail/python/test/hail/helpers.py`
- `rg -n "def test_init_hail_context_twice|def test_table_explode|def test_annotate|def test_list_batches_v2" hail/python/test/hail/test_context.py hail/python/test/hail/test_randomness.py hail/python/test/hail/table/test_table.py batch/test/test_batch.py`

## Source entry points
- `hail/python/test/hail/conftest.py` | symbols: `init_hail`, `init_query_on_batch`, `pytest_collection_modifyitems`
- `hail/python/test/hail/helpers.py` | symbols: `hl_init_for_test`, `test_timeout`, `with_flags`, `skip_unless_spark_backend`
- `hail/python/test/hail/test_context.py` | symbols: `test_init_hail_context_twice`, `test_fast_restarts_feature`
- `hail/python/test/hail/test_randomness.py` | symbols: `test_table_explode`, `test_matrix_table_entries`
- `hail/python/test/hail/table/test_table.py` | symbols: `test_annotate`, `test_query_table`, `test_table_randomness_union`
- `batch/test/test_batch.py` | symbols: `test_job`, `test_list_batches_v2`, `test_list_jobs_v2`
- `hail/python/hail/context.py` | symbols: `reset_global_randomness`, `init`
- `hail/python/hailtop/batch/backend.py` | symbols: `ServiceBackend._async_run`, `Backend.close`

## Function-level behavior checks
1. Validate backend fixture behavior in `hail/python/test/hail/conftest.py` before interpreting test skips or backend mismatches.
2. Validate helper decorators/utilities in `hail/python/test/hail/helpers.py` before modifying test timing or flag behavior.
3. Validate failing behavior in nearest test function before broadening scope.

## Validation checkpoints
- Every test recommendation maps to a concrete test function and fixture entry point.
- Backend-sensitive tests reference both fixture setup and backend implementation symbols.
