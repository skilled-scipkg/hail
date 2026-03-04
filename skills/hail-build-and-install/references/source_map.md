# hail source map: Build and Install

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "^(install-dev-requirements|generate-pip-lockfiles|check-pip-requirements):" Makefile`
- `rg -n "^(install-editable|pytest|pytest-qob|install-on-cluster|hail-docs-do-not-render-notebooks):" hail/Makefile`
- `rg -n "def init\(|def stop\(|class ServiceBackend|def deploy\(|def set\(" hail/python/hail/context.py hail/python/hail/backend/service_backend.py hail/python/hailtop/hailctl/dev/cli.py hail/python/hailtop/hailctl/dev/config.py`

## Source entry points
- `Makefile` | behavior entry: `install-dev-requirements`, `generate-pip-lockfiles`
- `hail/Makefile` | behavior entry: `install-editable`, `pytest`, `pytest-qob`, `install-on-cluster`
- `hail/python/hail/context.py` | symbols: `init`, `init_spark`, `init_local`, `stop`
- `hail/python/hail/backend/backend.py` | symbols: `local_jar_information`, `Backend.execute`
- `hail/python/hail/backend/service_backend.py` | symbols: `ServiceBackend.__init__`, `ServiceBackend.stop`, `ServiceBackend._rpc`
- `hail/python/hailtop/hailctl/dev/cli.py` | symbols: `deploy`
- `hail/python/hailtop/hailctl/dev/config.py` | symbols: `set`, `list`
- `hail/python/hailtop/hailctl/batch/initialize.py` | symbols: `async_basic_initialize`, `setup_new_remote_tmpdir`, `initialize_gcp`
- `batch/batch/driver/main.py` | symbols: `run`, `monitor_instances`
- `docker/third-party/Makefile` | behavior entry: `copy`

## Function-level behavior checks
1. Confirm command availability and prerequisites from Makefile targets before recommending build commands.
2. Confirm backend initialization and teardown behavior (`init`, `stop`, `ServiceBackend.stop`) for install smoke checks.
3. Confirm dev deploy/config behavior in `hailctl dev` code paths before suggesting service workflow commands.

## Validation checkpoints
- Build/install advice references existing Makefile targets.
- Environment and backend assumptions are backed by code-level initialization paths.
