# FastDiff V2

**Exact reconciliation for large datasets. Bounded-memory processing. Results you can replay.**

FastDiff V2 is a deterministic reconciliation system for comparing two data states by a declared key and selected typed fields. It turns large, unsorted exports into exact `CHANGED`, `ONLY_A` and `ONLY_B` results, with schema differences, fixed-point financial totals and a retained evidence bundle for offline verification.

External merge sorting and spill-to-disk let the Extended workflow process inputs larger than its configured memory budget. A local, binary-first deployment model keeps sensitive datasets and reconciliation artifacts under the operator's control.

## One workflow, from source to verified result

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

| Capability | What it delivers |
| --- | --- |
| Exact row reconciliation | Keyed `CHANGED`, `ONLY_A`, `ONLY_B` and `IDENTICAL` results over selected normalized fields |
| Large, unsorted inputs | Bounded chunks, external merge sorting and disk spill, with an explicit process memory budget |
| Acquisition and normalization | Configured CSV/JSON sources, optional HTTP GET / read-only GraphQL GET, explicit field mappings and retained snapshots |
| Schema comparison | Field, type, nullability and key differences between explicitly declared schemas |
| Financial reconciliation | Exact fixed-point amounts and grouped totals by account, currency or other declared dimensions |
| CI fast-fail | Full input validation and sorting, then row comparison up to the configured difference limit |
| Deterministic evidence | Result artifacts, manifests and SHA-256 hashes that bind the retained bundle for integrity checks and replay |
| Offline verification | Local integrity checking and result reconstruction from retained inputs |

## Precise answers to operational questions

Reconcile inventory snapshots, validate migration exports, compare ledger states or track changes in explicitly mapped blockchain-derived data. Define the entity identity once, select the fields that matter, and obtain an exact delta within that comparison contract.

| Result | Meaning |
| --- | --- |
| `IDENTICAL` | The same key has equal selected, normalized fields |
| `CHANGED` | The same key has different selected, normalized fields |
| `ONLY_A` | The key exists only in A |
| `ONLY_B` | The key exists only in B |

Extended rejects duplicate, empty and null canonical keys, including collisions introduced by normalization. Row results, schema differences and financial totals remain distinct so each answers its own question.

## A focused product architecture

| Component | Role |
| --- | --- |
| Core | Streaming comparison of already sorted files |
| Connectors | Source acquisition, explicit normalization and retained snapshots |
| Extended | CSV, TSV, JSON, JSONL, canonical connector CSV and read-only SQLite exports; external sort, schema comparison, financial reconciliation and CI |

FastDiff is designed for proprietary binary delivery and local operation. Local-file comparison and offline replay keep datasets on the operator's machine; optional acquisition contacts the endpoints the operator configures. See [data handling](PRIVACY.md) for bundle retention and access controls.

## Explore the documentation

- [Documentation guide](docs/README.md) — architecture, workflow and operational contracts
- [Synthetic ledger walkthrough](docs/WORKFLOW.md) — decimal normalization, a changed row and an exact USD 0.05 total difference
- [Comparison contract](docs/CONTRACT.md) — identity, resources, CI semantics and verification
- [Release notes](RELEASE_NOTES.md) — component versions and delivery status
- [Package verification](docs/VERIFY.md), [security](SECURITY.md) and [licensing](docs/LICENSING.md)

## Scope / Current release status

This release provides documentation and synthetic examples. **No production binary is currently published in FastDiff-2.** Binary delivery awaits final executable qualification, approved signing/trust, production licensing and commercial terms. V2 identifies the product generation; component versions are listed in the [release notes](RELEASE_NOTES.md).

- **Formats:** the documented version supports the inputs listed above. Native Parquet/Avro/ORC and PostgreSQL/MySQL adapters are outside this version's scope.
- **Scale:** external sorting supports data beyond the configured memory budget. The current Windows CLI has a 64–1024 MiB process budget and a ten-minute operation deadline; achievable input size depends on records, I/O and available disk. See [resource limits](docs/CONTRACT.md#large-inputs).
- **Evidence:** hashes establish byte integrity; offline replay is product verification, not third-party certification. Retain a trusted manifest hash separately from the bundle.
- **Source consistency:** network pagination is not an atomic snapshot. Use immutable exports when snapshot consistency matters; network acquisition has separate limits.

The [contract](docs/CONTRACT.md) defines the complete interpretation of results. Earlier releases in [FastDiff](https://github.com/cxclrfx/FastDiff) retain their own versions and terms.

Copyright (c) 2026 cxclrfx. See [LICENSE.txt](LICENSE.txt).
