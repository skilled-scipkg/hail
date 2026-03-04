---
name: hail-build-and-install
description: This skill should be used for Hail contributor builds, editable installs, package/service boundaries, and common build failure recovery.
---

# hail: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for source builds, editable installs, docs builds, and service-dev environment setup.
- Route to `hail-getting-started` for end-user pip installation only.
- Route to `hail-test` for deep test-selection strategy.
- Route to `hail-troubleshooting` for runtime/auth/cluster incidents.

### Triage questions
- Is this local contributor build, cluster build, or service deployment?
- Is editable install required (`make -C hail install-editable`) or wheel install?
- Were Python dependencies or service dependencies changed?
- Is the change in Query compiler/runtime, Batch services, or both?
- Are Java 11, Python 3.10+, and optional native deps installed?

### Canonical workflow
1. Install repo dev dependencies and tooling. See:
   - `Makefile`
   - `dev-docs/development-process.md`
2. Configure local developer tools (`pre-commit`, cloud CLIs, kubectl, docker) when service work is needed.
3. Build and install Query in editable mode:
   - `hail/Makefile`
   - `hail/python/hail/docs/getting_started_developing.rst`
4. Run focused tests before broad suites.
5. For cluster installs, use `install-on-cluster` flow in `hail/python/hail/docs/install/other-cluster.rst`.
6. If dependency files changed, regenerate lockfiles via `make generate-pip-lockfiles`.

### Minimal working example
```bash
make install-dev-requirements
make -C hail install-editable
make -C hail pytest PYTEST_TARGET=test/hail/test_context.py
```

### Pitfalls and fixes
- Cluster install fails after partial native build: run `make clean`, retry `make install-on-cluster`.
- `HAIL_COMPILE_NATIVES=1` without lz4 headers: install `liblz4-dev` first.
- Dependency edits without lockfile refresh: run `make generate-pip-lockfiles`.
- Third-party image copy failures: verify context and registry auth first:
  - `dev-docs/services/setting_the_kubectl_context.md`
  - `dev-docs/services/connecting_docker_to_container_registry_creds.md`
  - `dev-docs/services/updating-third-party-images.md`
- Batch UI local dev Tailwind issue: follow `dev-docs/services/services-development-faq.md`.

### Convergence and validation checks
- `make -C hail install-editable` completes and `python -c 'import hail; print(hail.version())'` succeeds.
- At least one focused Python test passes (`hail/python/test/hail/test_context.py` or touched tests).
- If deps changed, lockfiles are regenerated with corresponding dependency edits.
- If docs changed, docs target passes (`make -C hail hail-docs-do-not-render-notebooks`).

## Primary documentation references
- `dev-docs/development-process.md`
- `dev-docs/pip-dependencies.md`
- `hail/python/hail/docs/getting_started_developing.rst`
- `hail/python/hail/docs/install/other-cluster.rst`
- `dev-docs/services/services-development-faq.md`
- `dev-docs/services/updating-third-party-images.md`
- `dev-docs/services/setting_the_kubectl_context.md`
- `dev-docs/services/connecting_docker_to_container_registry_creds.md`
- `dev-docs/services/docker-hub-cache.md`
- `hail/python/hail/docs/style-guide.txt`

## Package/component boundaries
- Query Python API: `hail/python/hail`
- Query JVM/compiler/runtime: `hail/hail/src`
- Batch Python API/client: `hail/python/hailtop/batch`, `hail/python/hailtop/batch_client`
- Batch service: `batch/batch`
- JVM entryway for Query-on-Batch jobs: `batch/jvm-entryway/src`

## Source-code entry links (when docs are insufficient)
- `Makefile`
- `hail/Makefile`
- `hail/python/hail/backend/backend.py`
- `hail/python/hail/backend/service_backend.py`
- `hail/python/hailtop/hailctl/dev/cli.py`
- `hail/python/hailtop/hailctl/dev/config.py`
- `batch/batch/driver/main.py`
- `batch/batch/front_end/query/query_v2.py`
- `batch/jvm-entryway/src/is/hail/JVMEntryway.java`
- `docker/third-party/Makefile`

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
