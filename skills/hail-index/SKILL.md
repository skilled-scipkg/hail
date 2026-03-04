---
name: hail-index
description: This skill should be used when users ask how to use Hail and you must route to the right docs-first topic skill before any source-code deep dive.
---

# hail Skills Index

## Route the request
- Start with the smallest matching topic skill below.
- Keep answers docs-first and topic-correct; do not jump to source unless the selected topic's primary docs and its references doc map are insufficient.

## Fast triage by request type
- Query/Table/MatrixTable/expressions/API semantics -> `hail-api-and-scripting`
- Batch scripting, `hailtop.batch`, local vs service backend behavior -> `hail-api-and-scripting`
- First-time setup, install, first runnable analysis, tutorial notebook entry points -> `hail-getting-started`
- Contributor/developer build, editable installs, service dev env, component boundaries -> `hail-build-and-install`
- Runtime/auth/cloud/cluster failures, CI/release incidents, flaky diagnosis -> `hail-troubleshooting`
- Test selection, backend-specific test execution, regression checks -> `hail-test`
- Architecture and internal lifecycle docs (IR/lowering/randomness/ops runbooks) -> `hail-dev-docs`
- Full worked pipelines and cookbook-style runnable examples -> `hail-examples-and-tutorials`
- Advanced sparse topics consolidated from single-doc areas -> `hail-advanced-topics`
- Workflow/execution-graph simulation questions not covered above -> `hail-simulation-workflows`

## Topic skills
- `hail-getting-started`: install/runtime prerequisites, first query, tutorials
- `hail-build-and-install`: local and cluster builds, editable installs, service dev setup
- `hail-api-and-scripting`: Hail Query API and Hail Batch Python API
- `hail-test`: test strategy, commands, fixtures, backend-specific runs
- `hail-dev-docs`: internals and service operation runbooks
- `hail-troubleshooting`: diagnosis, auth/cloud/runtime failure handling
- `hail-examples-and-tutorials`: cookbook and tutorial workflows
- `hail-simulation-workflows`: simulation DAG design, resource sizing, reproducibility checks
- `hail-advanced-topics`: consolidated one-doc specialist topics

## Required escalation order
1. Primary docs in the selected topic `SKILL.md`
2. Selected topic references doc map (`<topic-skill>/references/doc_map.md`)
3. Selected topic references source map (`<topic-skill>/references/source_map.md`)

## Runnable-example routing
- If user asks for runnable examples, prioritize:
  - `hail/python/hail/docs/tutorials`
  - `hail/python/hailtop/batch/docs/tutorial.rst`
  - `hail/python/hailtop/batch/docs/cookbook`
- If user asks for behavior validation/regression checks, route to tests:
  - `hail/python/test`
  - `hail/hail/test`
  - `batch/test`

## Global source roots (only after docs escalation)
- `hail/python/hail`
- `hail/python/hailtop`
- `hail/hail/src`
- `batch/batch`
- `batch/jvm-entryway/src`
