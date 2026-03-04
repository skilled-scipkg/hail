---
name: hail-dev-docs
description: This skill should be used for Hail internal architecture and operations docs (query lifecycle, randomness, service ops runbooks, and platform internals).
---

# hail: Dev Docs

## High-Signal Playbook
### Route conditions
- Use this skill for internals questions (IR/lowering/randomness), service runbooks, and platform architecture context.
- Route to `hail-build-and-install` for concrete environment and build setup.
- Route to `hail-troubleshooting` for active incident handling.
- Route to `hail-api-and-scripting` for user-facing API behavior questions.

### Triage questions
- Is this Query internals (IR/backend/randomness) or service operations?
- Is this compiler/runtime-side or Batch driver/front-end-side?
- Is cloud context GCP or Azure?
- Is the ask architectural explanation or operational remediation?

### Canonical workflow
1. Identify doc class first:
   - Query internals: `dev-docs/hail-query/hail-query-lifecycle.md`, `dev-docs/hail-query/randomness.md`
   - Ops runbooks: `dev-docs/services/batch/operation.md` and service docs
2. Reproduce minimal IR when needed (`_ir`, `_tir`) on tiny pipelines.
3. For service operations, verify kubectl context and registry auth before mutation.
4. For capacity/perf questions, use driver CPU, latency, and quota guidance from `dev-docs/services/batch/operation.md`.
5. Escalate to source when docs describe behavior but not implementation details.

### Minimal working example
```python
import hail as hl

t = hl.utils.range_table(100)
print(t._tir)
cond = t.idx % 7 < 4
print(cond._ir)
print(t.filter(cond)._tir)
```

### Pitfalls and fixes
- Assuming eager expression execution: Hail expression trees are lazy until action.
- Treating randomness behavior as nondeterministic bug without UID-model review.
- Running service operations under wrong cluster context.
- Diagnosing Batch overload from errors only; include utilization and queue-latency signals.

### Convergence and validation checks
- IR printout reflects expected transform ordering and shape.
- Context/auth checks pass before destructive operations.
- Ops recommendation maps to one exact doc path and one concrete metric/signal.

## Primary documentation references
- `dev-docs/hail-query/hail-query-lifecycle.md`
- `dev-docs/hail-query/randomness.md`
- `dev-docs/services/setting_the_kubectl_context.md`
- `dev-docs/services/connecting_docker_to_container_registry_creds.md`
- `dev-docs/services/batch/operation.md`
- `dev-docs/hail-overview.md`
- `dev-docs/gvs.md`
- `dev-docs/algolia.md`

## Source-code entry links (when docs are insufficient)
- `hail/python/hail/backend/backend.py`
- `hail/python/hail/backend/service_backend.py`
- `hail/python/hail/ir/table_ir.py`
- `batch/batch/front_end/query/query_v2.py`
- `batch/batch/front_end/query/operators.py`
- `batch/batch/driver/main.py`
- `batch/batch/driver/resource_manager.py`
- `batch/batch/driver/canceller.py`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
