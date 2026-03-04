---
name: hail-advanced-topics
description: This skill should be used for consolidated advanced Hail topics that previously had single-doc coverage (new-engineer context, Query-on-Batch internals, and identity management).
---

# hail: Advanced Topics

## Scope
- Use this skill for advanced context that does not fit a broader topic skill:
  - new-engineer architecture boundaries
  - Query-on-Batch client/driver/worker internals
  - identity and auth model across user machine, jobs, and services

## Route conditions
- Route to `hail-getting-started` for end-user setup/onboarding.
- Route to `hail-api-and-scripting` for API semantics and scripting workflows.
- Route to `hail-troubleshooting` for active runtime/auth incidents.
- Route to `hail-dev-docs` for broader runbooks outside this focused trio.

## Primary documentation references
- `dev-docs/hail-for-new-engineers.md`
- `dev-docs/hail-query/query-on-batch.md`
- `dev-docs/services/auth/identity-management.md`

## Practical workflow
1. Pick the subtopic first (architecture, QoB internals, or identity).
2. Answer from the matching primary doc.
3. If behavior detail is missing, inspect source entry points.
4. Validate claim with one concrete symbol or command hit.

## Quick checks
- `rg -n "parse_list_batches_query_v2|parse_job_group_jobs_query_v2" batch/batch/front_end/query/query_v2.py`
- `rg -n "auth_flow|copy_paste_login|get_userinfo" hail/python/hailtop/hailctl/auth/login.py hail/python/hailtop/auth/auth.py`
- `rg -n "main\(|finishFutures|throwableToString" batch/jvm-entryway/src/is/hail/JVMEntryway.java`

## Source-code entry links (when docs are insufficient)
- `hail/python/hail/backend/service_backend.py`
- `hail/python/hail/backend/backend.py`
- `batch/batch/front_end/query/query_v2.py`
- `batch/jvm-entryway/src/is/hail/JVMEntryway.java`
- `hail/python/hailtop/hailctl/auth/login.py`
- `hail/python/hailtop/auth/auth.py`
- `auth/auth/auth.py`
- `auth/auth/driver/driver.py`

## Validation checkpoints
- Query parser interpretation is verified with a direct function read in `batch/batch/front_end/query/query_v2.py`.
- Auth flow assertion is verified in both CLI and auth-client code paths.
- JVM entryway claims are tied to explicit methods in `batch/jvm-entryway/src/is/hail/JVMEntryway.java`.

## Escalation order
1. Primary docs above
2. `references/doc_map.md`
3. `references/source_map.md`
