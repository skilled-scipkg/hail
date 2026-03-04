# hail source map: Troubleshooting

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "def auth_flow|def async_login|def async_basic_initialize|def setup_existing_remote_tmpdir" hail/python/hailtop/hailctl/auth/login.py hail/python/hailtop/hailctl/batch/initialize.py`
- `rg -n "def _rpc\(|def stop\(|def remote_tmpdir|def init\(|def current_backend|def debug_info\(" hail/python/hail/backend/service_backend.py hail/python/hail/context.py`
- `rg -n "def run\(|def monitor_instances|class CloudResourceManager|class Canceller|def parse_list_batches_query_v2" batch/batch/driver/main.py batch/batch/driver/resource_manager.py batch/batch/driver/canceller.py batch/batch/front_end/query/query_v2.py`

## Source entry points
- `hail/python/hailtop/hailctl/auth/login.py` | symbols: `auth_flow`, `async_login`
- `hail/python/hailtop/hailctl/batch/initialize.py` | symbols: `async_basic_initialize`, `initialize_gcp`, `setup_existing_remote_tmpdir`
- `hail/python/hail/backend/service_backend.py` | symbols: `ServiceBackend._rpc`, `ServiceBackend.validate_file`, `ServiceBackend.stop`
- `hail/python/hail/context.py` | symbols: `init`, `current_backend`, `debug_info`
- `batch/batch/driver/main.py` | symbols: `validate`, `monitor_instances`, `run`
- `batch/batch/driver/resource_manager.py` | symbols: `CloudResourceManager`, `VMStateRunning`, `VMStateTerminated`
- `batch/batch/driver/canceller.py` | symbols: `Canceller.cancel_cancelled_ready_jobs_loop_body`, `Canceller.cancel_cancelled_running_jobs_loop_body`
- `batch/batch/front_end/query/query_v2.py` | symbols: `parse_list_batches_query_v2`, `parse_job_group_jobs_query_v2`
- `ci/ci/ci.py` | symbols: `filter_jobs`, `storage_uri_to_url`, `run`

## Function-level behavior checks
1. Validate auth/config failures in hailctl login and initialize code before service-side assumptions.
2. Validate backend/runtime failures through `ServiceBackend` and `context` symbols before driver deep dives.
3. Validate scheduler/cancellation/query symptoms via driver and query parser functions.

## Validation checkpoints
- Repro symptom is mapped to one of: auth/init, backend runtime, driver/cancel, query parser, or CI layer.
- Escalation includes explicit file + symbol candidates, not only package-level paths.
