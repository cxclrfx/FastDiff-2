# Release notes

## v2-docs.1 — documentation package — 2026-09-21

Initial public-facing FastDiff V2 documentation, operational boundaries, security/privacy information, a synthetic ledger example and SHA-256 checksums.

**Release type:** documentation only. This tag is not executable version 2.0.0, a production software release or an independent qualification result.

### Component version map

| Product layer | Component version |
| --- | --- |
| Core | 0.2.1 |
| Connectors | 0.2.0 |
| Extended | 0.1.0 |

V2 is the product-generation name. Configuration and bundle versions retain the component-specific contracts.

### Binary availability

No EXE or commercial software archive is included in this release. Production binary delivery remains pending final executable qualification, the approved signing/trust process, production licensing and final commercial terms.

No production runtime test was performed as part of this documentation release. No benchmark, platform certification or independent closure claim is made.

### Documented scope

External sorting of unsorted local inputs; explicitly mapped sources and keys; declared-schema comparison; exact fixed-point reconciliation; bounded row-difference CI output; retained snapshots and offline replay.

### Boundaries

- Extended keys must be unique, nonempty and non-null.
- Schema comparison uses declarations, not automatic discovery or attestation.
- Network connectors have their own acquisition limits.
- CI validates and sorts complete inputs before limiting row comparison.
- No native Parquet/Avro/ORC or PostgreSQL/MySQL adapter is included.
- A valid replay may contain differences. Verification success is not dataset equality.

See [the contract](docs/CONTRACT.md).
