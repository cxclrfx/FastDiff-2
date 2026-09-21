# FastDiff V2

**Deterministic reconciliation of two data states, with local processing and offline replay.**

FastDiff compares records by an explicitly defined key and reports what stayed identical, what changed, and what exists on only one side. The extended workflow prepares unsorted inputs using external sorting and disk spill, then produces a result bundle that can be replayed locally.

> **Availability:** this repository is the public-facing documentation and synthetic example package. No production binary is distributed here yet. V2 names the product generation; it does not mean that the executable or configuration version is `2.0.0`. See [release status](RELEASE_NOTES.md).

## From inputs to a checkable result

```text
Declared sources + schema + key
              |
      Acquire / normalize
              |
  External sort / spill to disk
              |
       Reconcile A and B
              |
   Delta + manifest + snapshots
              |
       Offline verification
```

Optional network acquisition precedes the extended local comparison. Its limits differ from the external-sort stage.

| Result | Meaning |
| --- | --- |
| `IDENTICAL` | The same key has equal selected, normalized fields |
| `CHANGED` | The same key has different selected, normalized fields |
| `ONLY_A` | The key exists only in A |
| `ONLY_B` | The key exists only in B |

Duplicate, empty or null keys are rejected in the extended workflow. FastDiff does not silently collapse duplicate records.

## Capabilities

| Component | Scope |
| --- | --- |
| Core | Streaming comparison of already sorted files |
| Connectors | Configured CSV/JSON and optional HTTP GET / read-only GraphQL GET acquisition; normalization and retained snapshots |
| Extended | CSV, TSV, JSON, JSONL, canonical connector CSV and read-only SQLite exports; external sort and disk spill |
| Schema comparison | Differences between explicitly declared schemas, including fields, types, nullability and keys |
| Financial reconciliation | Exact fixed-point amounts and grouped totals without floating-point rounding or FX conversion |
| CI mode | Validate and sort complete inputs, then stop row comparison at a selected difference limit |
| Offline verification | Check bundle integrity and reconstruct results from retained inputs |

The product is intended for local binary delivery. The internal implementation is not included in this repository. Existing releases in [FastDiff](https://github.com/cxclrfx/FastDiff) retain their own versions and terms.

## Start here

- [Workflow and synthetic ledger example](docs/WORKFLOW.md)
- [Contracts, limits and interpretation](docs/CONTRACT.md)
- [Release notes and binary availability](RELEASE_NOTES.md)
- [Security](SECURITY.md) and [privacy](PRIVACY.md)
- [Repository terms](LICENSE.txt) and [binary licensing status](docs/LICENSING.md)
- [Verify this package](docs/VERIFY.md)

The [ledger fixture](examples/ledger/) is synthetic: one selected row is identical, one changes, and the grouped B-minus-A amount is USD 0.05. These are expected fixture results, not a claim that a production binary has passed release qualification.

## Where it fits

Compare inventory snapshots, migration exports, ledger extracts or explicitly mapped blockchain-derived datasets. Both sources must use the same intended entity identity and selected-field semantics.

FastDiff is not a database, interactive dataset viewer, blockchain indexer, wallet-identity classifier or financial audit opinion. Native Parquet/Avro/ORC, PostgreSQL and MySQL adapters are not included in the documented version.

## Correctness boundaries

- Equality is scoped to selected normalized fields and the declared key.
- Matching SHA-256 values establish byte integrity, not source truth, completeness or business correctness.
- Offline replay uses the product verifier; it is not independent certification.
- A self-consistent replacement of an entire bundle requires a separately retained trusted manifest hash to detect.
- Network pagination does not create an atomic snapshot. Use immutable exports when snapshot consistency matters.
- Bounded processing does not mean bounded disk usage or a limit on whole-machine RAM.

See [the contract](docs/CONTRACT.md) for the complete operational boundaries.

Copyright (c) 2026 cxclrfx. See [LICENSE.txt](LICENSE.txt).
