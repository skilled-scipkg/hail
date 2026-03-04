# hail source map: Advanced Topics

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "parse_list_batches_query_v2|parse_job_group_jobs_query_v2" batch/batch/front_end/query/query_v2.py`
- `rg -n "auth_flow|async_login|copy_paste_login|get_userinfo" hail/python/hailtop/hailctl/auth/login.py hail/python/hailtop/auth/auth.py`
- `rg -n "main\(|finishFutures|throwableToString" batch/jvm-entryway/src/is/hail/JVMEntryway.java`

## Source entry points
- `hail/python/hail/backend/service_backend.py` | symbols: `ServiceBackend.__init__`, `ServiceBackend._rpc`, `ServiceBackend.remote_tmpdir`
- `hail/python/hail/backend/backend.py` | symbols: `Backend.execute`, `ActionTag`, `Backend.register_ir_function`
- `batch/batch/front_end/query/query_v2.py` | symbols: `parse_list_batches_query_v2`, `parse_job_group_jobs_query_v2`
- `batch/jvm-entryway/src/is/hail/JVMEntryway.java` | symbols: `main`, `finishFutures`, `throwableToString`
- `hail/python/hailtop/hailctl/auth/login.py` | symbols: `auth_flow`, `async_login`
- `hail/python/hailtop/auth/auth.py` | symbols: `hail_credentials`, `copy_paste_login`, `get_userinfo`
- `auth/auth/auth.py` | symbols: `LocalAuthenticator`, `cleanup_session`, `run`
- `auth/auth/driver/driver.py` | symbols: `EventHandler`, `GSAResource`, `BillingProjectResource`

## Function-level behavior checks
1. Verify query-token parsing behavior in `parse_list_batches_query_v2` before interpreting query syntax claims.
2. Verify user-login and token exchange behavior across `auth_flow` and `copy_paste_login` before diagnosing auth drift.
3. Verify JVM entryway lifecycle (`main` and `finishFutures`) before making cancellation or completion claims.

## Validation checkpoints
- Each behavior claim is tied to one symbol from this map.
- Auth and QoB lifecycle claims are cross-checked in both Python and service/JVM code.
