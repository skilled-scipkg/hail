# hail documentation map: Test

Use this map after reading `skills/hail-test/SKILL.md`.

## Test process docs
- `dev-docs/development-process.md`
- `dev-docs/services/flaky_tests.md`
- `hail/python/hail/docs/getting_started_developing.rst`
- `hail/Makefile`

## Python test framework entry docs
- `hail/python/test/hail/conftest.py`
- `hail/python/test/hail/helpers.py`
- `hail/python/test/hail/test_context.py`
- `hail/python/test/hail/test_randomness.py`
- `hail/python/test/hail/table/test_table.py`

## Service and integration test entry docs
- `batch/test/test_batch.py`
- `hail/hail/test/src/is/hail/backend/ServiceBackendSuite.scala`

## Test data references
- `hail/hail/test/resources/sample.vcf.mt/README.txt`
- `hail/hail/test/resources/vds/1kg_chr22_5_samples.vds/variant_data/README.txt`

## Escalation hints
- Prefer focused tests nearest changed behavior, then broaden coverage.
- Use `source_map.md` for fixture and backend behavior internals.
