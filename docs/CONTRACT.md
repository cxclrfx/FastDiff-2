# Comparison contract and operational scope

FastDiff produces exact results within an explicit identity, normalization and resource contract. This document defines how to interpret row differences, schema results, financial totals and replay evidence.

## Identity and normalization

Declare the entity, selected typed fields, source mappings and ordered key. The same key must denote the same intended entity in both sources. Supported selected types include string, unsigned integer, exact decimal, boolean and EVM address.

Extended rejects empty/null/duplicate canonical keys, including duplicates introduced by normalization. It does not provide duplicate-multiplicity reconciliation. Equality refers only to selected normalized fields; ignored fields remain outside the result.

## Large inputs

Extended normalizes and sorts inputs using bounded chunks and disk merges. The Windows CLI exposes a memory budget from 64 to 1024 MiB and enforces a process private-committed-memory ceiling. This is not a ceiling on shared libraries, the OS file cache or total machine RAM. Oversized records and invalid inputs fail. The current CLI also applies a ten-minute operation deadline; large-data capacity is constrained by that deadline and available I/O.

Raw snapshots, normalized files, merge runs and the full delta require disk space. There is no disk quota guarantee. Legacy network acquisition retains separate page/row limits and must not be described as the same external-sort memory contract.

CSV/TSV require headers and one physical line per record. JSON input requires valid encoding and unambiguous field names. Select explicit mappings; there is no automatic schema inference.

## SQLite

Use a quiescent, checkpointed database export. Comparison reads a local copy under read-only restrictions. WAL/journal inputs, writes, extension loading and unsupported query constructs are rejected. INTEGER or TEXT outputs are required for exact amounts; floating-point query output is unsuitable.

Copy/hash checks do not prove that a changing upstream database was captured atomically.

## Schema and financial results

Schema comparison requires both explicitly declared schemas. Without declarations its status is NOT_APPLICABLE. Selected rows may compare equal while declared schemas differ.

Financial reconciliation groups exact integer-scaled amounts by explicitly selected dimensions including currency. Nonzero excess precision fails; there is no silent rounding or FX conversion. Equal totals do not prove equal rows or financial correctness.

## CI and exit status

Extended compare/CI: 0 means no reported differences, 1 means differences, 2 means invalid/incomplete/error. External termination may have an OS-specific status. These codes do not redefine historical Core/Connectors commands.

CI validates and sorts every input record before stopping row comparison at the configured difference limit. Its row counts may describe only an observed prefix; schema and financial results remain separate. A partial row comparison is not an exhaustive delta.

## Verification and trust

Extended verify checks expected artifacts and reconstructs results from retained inputs. Exit 0 means valid replay, even when the datasets differ. Preserve the printed manifest SHA-256 separately and provide it during verification when checking an external anchor.

A checksum is not an attestation of source truth, declaration authority, completeness, atomicity or independent correctness. A completely replaced self-consistent bundle needs an external trusted anchor to detect.

Interrupted runs remain incomplete. Retry in a new output directory; do not promote partial artifacts into successful results.

## Supported integration scope

Extended accepts CSV, TSV, JSON, JSONL, canonical connector CSV and read-only SQLite exports. Native Parquet/Avro/ORC and PostgreSQL/MySQL adapters are outside the documented version. CSV/JSON and optional HTTP GET / read-only GraphQL GET acquisition are provided through configured Connectors paths.

FastDiff reconciles supplied data states. Database service, interactive data browsing, blockchain indexing, wallet-identity classification and financial audit opinions are outside its role. Selected keys and mappings must express the same intended entity and field semantics on both sides.

Network pagination is not an atomic snapshot. Use immutable exports or an upstream snapshot mechanism when source consistency matters.

Offline replay uses the product verifier and is not independent or third-party certification. Hash equality establishes byte integrity, rather than source truth or business correctness. Financial reconciliation performs no FX conversion. The memory ceiling applies to process private committed memory, while disk requirements and whole-machine memory remain separate resource concerns.
