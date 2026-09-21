# Release notes

## v2-docs.2 — reconciliation system guide — 2026-09-21

FastDiff V2 brings exact row reconciliation, declared-schema comparison, fixed-point financial totals and offline replay into a local workflow for large datasets. External merge sorting and spill-to-disk prepare unsorted inputs within an explicit process memory budget; CI mode limits row comparison after complete input validation and sorting.

This documentation revision sharpens the product overview, adds a documentation guide and aligns workflow, privacy, verification and delivery text around that architecture. Comparison semantics, component versions and synthetic fixtures are unchanged. The original `v2-docs.1` tag and archive remain the prior documentation snapshot.

### Scope / Current release status

**Release type:** documentation and synthetic examples. No production binary is currently published in FastDiff-2. The ZIP contains the repository package files and per-file SHA-256 checksums.

Production binary delivery awaits final executable qualification, approved signing/trust, production licensing and final commercial terms. This editorial release includes no production runtime execution, benchmark, platform certification or independent qualification result.

V2 names the product generation. Documentation tags, executable versions, configuration versions and bundle contracts are distinct.

### Component version map

| Product layer | Component version |
| --- | --- |
| Core | 0.2.1 |
| Connectors | 0.2.0 |
| Extended | 0.1.0 |

Configuration and bundle versions retain the component-specific contracts.

### Operational scope

- Extended supports CSV, TSV, JSON, JSONL, canonical connector CSV and read-only SQLite exports. Native Parquet/Avro/ORC and PostgreSQL/MySQL adapters are outside the documented version.
- Keys must be unique, nonempty and non-null after normalization. Equality covers selected normalized fields.
- Schema comparison uses explicit declarations. Financial totals use exact fixed-point amounts with declared grouping and currency; FX conversion is outside scope.
- External sorting uses a configured process memory budget. The current Windows CLI exposes 64–1024 MiB and a ten-minute operation deadline; input capacity depends on record size, I/O and available disk.
- Network connectors retain their own acquisition limits. Pagination is not an atomic source snapshot.
- CI validates and sorts complete inputs before limiting row comparison. A limited comparison reports an observed prefix, rather than an exhaustive row delta.
- Offline replay checks integrity and reconstructs results using the product verifier. It is not third-party certification; successful replay may contain differences. A separately retained trusted manifest hash anchors bundle identity.

See [the comparison contract](docs/CONTRACT.md) for full resource and trust boundaries.

## v2-docs.1 — initial documentation package — 2026-09-21

Introduced the FastDiff V2 product overview, component/version map, operational contract, security/privacy information, synthetic ledger example and SHA-256 checksums. This documentation-only release included no production executable or runtime qualification result. Its original tag and release assets are retained unchanged.
