# hail source map: Dev Docs

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "class Table|class TableFilter|class TableMapRows|class TableKeyBy" hail/python/hail/ir/table_ir.py`
- `rg -n "def execute\(|def register_ir_function\(|def _rpc\(" hail/python/hail/backend/backend.py hail/python/hail/backend/service_backend.py`
- `rg -n "def parse_list_batches_query_v2|def get_operator|def monitor_instances|class CloudResourceManager" batch/batch/front_end/query/query_v2.py batch/batch/front_end/query/operators.py batch/batch/driver/main.py batch/batch/driver/resource_manager.py`

## Source entry points
- `hail/python/hail/ir/table_ir.py` | symbols: `TableRange`, `TableFilter`, `TableMapRows`, `TableKeyByAndAggregate`
- `hail/python/hail/backend/backend.py` | symbols: `Backend.execute`, `Backend.register_ir_function`, `ActionTag`
- `hail/python/hail/backend/service_backend.py` | symbols: `ServiceBackend._rpc`, `ServiceBackend._cancel_on_ctrl_c`, `ServiceBackend.get_flags`
- `batch/batch/front_end/query/query_v2.py` | symbols: `parse_list_batches_query_v2`, `parse_job_group_jobs_query_v2`
- `batch/batch/front_end/query/operators.py` | symbols: `get_operator`, `pad_maybe_operator`, `EqualExactMatchOperator`
- `batch/batch/driver/main.py` | symbols: `monitor_instances`, `validate`, `run`
- `batch/batch/driver/resource_manager.py` | symbols: `CloudResourceManager`, `VMStateRunning`, `VMStateTerminated`
- `batch/batch/driver/canceller.py` | symbols: `Canceller.cancel_cancelled_ready_jobs_loop_body`, `Canceller.cancel_orphaned_attempts_loop_body`

## Function-level behavior checks
1. For IR/lowering claims, map to a concrete class in `hail/python/hail/ir/table_ir.py`.
2. For backend execution claims, map to `Backend.execute` and `ServiceBackend._rpc`.
3. For Batch query or operations claims, map to parser/operator and driver manager symbols.

## Validation checkpoints
- Each architecture or ops statement references one symbol from this map.
- Query parsing and driver behavior claims are validated in separate files, not inferred from one layer.
