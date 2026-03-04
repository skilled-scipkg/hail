# hail source map: Getting Started

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "def init\(|def init_spark\(|def init_local\(|def current_backend\(|def stop\(" hail/python/hail/context.py`
- `rg -n "class SparkBackend|class ServiceBackend" hail/python/hail/backend/spark_backend.py hail/python/hail/backend/service_backend.py`
- `rg -n "def new_job|def run\(|def auth_flow|def async_basic_initialize" hail/python/hailtop/batch/batch.py hail/python/hailtop/hailctl/auth/login.py hail/python/hailtop/hailctl/batch/initialize.py`

## Source entry points
- `hail/python/hail/context.py` | symbols: `init`, `init_spark`, `init_local`, `current_backend`, `stop`
- `hail/python/hail/backend/spark_backend.py` | symbol: `SparkBackend`
- `hail/python/hail/backend/service_backend.py` | symbols: `ServiceBackend.__init__`, `ServiceBackend.remote_tmpdir`, `ServiceBackend.stop`
- `hail/python/hailtop/batch/batch.py` | symbols: `Batch.new_job`, `Batch.read_input`, `Batch.run`
- `hail/python/hailtop/batch/backend.py` | symbols: `LocalBackend`, `ServiceBackend`, `Backend.close`
- `hail/python/hailtop/hailctl/auth/login.py` | symbols: `auth_flow`, `async_login`
- `hail/python/hailtop/hailctl/batch/initialize.py` | symbols: `async_basic_initialize`, `setup_existing_remote_tmpdir`, `setup_new_remote_tmpdir`
- `hail/python/test/hail/test_context.py` | symbols: `test_init_hail_context_twice`, `test_fast_restarts_feature`

## Function-level behavior checks
1. Validate startup behavior in `hail/python/hail/context.py` before attributing setup issues to docs.
2. Validate backend selection claims by tracing `current_backend` and backend class usage.
3. Validate auth/init wizard behavior with `auth_flow` and `async_basic_initialize`.

## Validation checkpoints
- First-run claims tie to one initialization symbol and one backend symbol.
- Config/auth guidance is traceable to hailctl login/initialize code.
