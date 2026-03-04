---
name: hail-troubleshooting
description: This skill should be used for Hail auth/cloud/runtime failures, CI/release incidents, and fast diagnosis with test-backed sanity checks.
---

# hail: Troubleshooting

## High-Signal Playbook
### Route conditions
- Use this skill for failing runs, auth issues, cloud/runtime incidents, CI/release breakage, and flaky-test diagnosis.
- Route to `hail-getting-started` if issue is incomplete base setup.
- Route to `hail-build-and-install` for build/dependency installation failures.
- Route to `hail-test` for deep test design/selection work.

### Triage questions
- Is this query failure, Batch-service failure, CI failure, or release failure?
- Which backend (`spark` or `batch`) and which cloud?
- Is impact isolated or system-wide?
- What is the exact failing command, job/batch ID, and timestamp?
- What changed recently (version, deploy, credentials, quota, config)?

### Canonical workflow
1. Assign severity using `dev-docs/hail-production-issues.md`.
2. Capture minimal repro plus backend/cloud/config/auth context.
3. Run fast sanity checks (auth, config, tiny query, tiny batch).
4. For infra incidents, follow runbooks:
   - `dev-docs/services/kubernetes-operations.md`
   - `dev-docs/services/batch/operation.md`
5. For flaky CI, use `dev-docs/services/flaky_tests.md`.
6. For release issues, apply `dev-docs/releasing.md`.
7. Escalate to source files only after runbooks and sanity checks.

### Minimal working example
```bash
hailctl auth login
hailctl config set query/backend batch
python - <<'PY'
import hail as hl
hl.init(backend='batch')
print(hl.version())
print(hl.utils.range_table(5).count())
PY
```

### Pitfalls and fixes
- Confusing Hail auth with cloud auth: `hailctl auth login` does not replace cloud provider credentials.
- Kubernetes/terraform drift issues: sync state per `dev-docs/services/kubernetes-operations.md`.
- Driver overload feedback loops: tune throughput and capacity with `dev-docs/services/batch/operation.md`.
- Release failures with temporary hold artifacts: follow `dev-docs/releasing.md` recovery steps.
- Hidden behavior changes after upgrade: verify against `hail/python/hail/docs/change_log.md`.

### Convergence and validation checks
- Minimal failure is reproducible (or resolution is demonstrated).
- Auth and config state are explicitly verified before deep debugging.
- One focused smoke test passes after fix.
- Incident has clear next action owner and code/doc evidence.

## Primary documentation references
- `dev-docs/hail-production-issues.md`
- `dev-docs/services/kubernetes-operations.md`
- `dev-docs/services/batch/operation.md`
- `dev-docs/services/flaky_tests.md`
- `dev-docs/releasing.md`
- `dev-docs/services/auth/identity-management.md`
- `dev-docs/services/ci/README.md`
- `hail/python/hail/docs/change_log.md`

## Test-backed sanity checks
- `make -C hail pytest PYTEST_TARGET=test/hail/test_context.py`
- `make -C hail pytest PYTEST_TARGET=test/hail/test_randomness.py`
- `make -C hail pytest PYTEST_TARGET=test/hail/table/test_table.py`
- `make -C hail pytest-qob NAMESPACE=default PYTEST_ARGS='-k service_backend'`

## Source-code entry links (when docs are insufficient)
- `hail/python/hailtop/hailctl/auth/login.py`
- `hail/python/hailtop/hailctl/batch/initialize.py`
- `hail/python/hail/backend/service_backend.py`
- `batch/batch/driver/main.py`
- `batch/batch/driver/resource_manager.py`
- `batch/batch/driver/canceller.py`
- `batch/batch/front_end/query/query_v2.py`
- `ci/ci/constants.py`
- `hail/python/hail/context.py`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
