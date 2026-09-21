# Workflow and synthetic ledger example

Turn two ledger states into an exact row delta and grouped financial totals, then verify the retained result offline. This walkthrough uses synthetic data to show the Extended comparison contract from input mapping to replay.

1. Prepare immutable local exports or acquire configured sources through Connectors.
2. Declare selected fields, explicit mappings and the identity key.
3. Compare into a new output directory.
4. Retain the complete bundle and store its manifest hash separately.
5. Replay the bundle offline, supplying that trusted hash.

## Ledger fixture

The files in [examples/ledger](../examples/ledger/) contain two synthetic records in each state.

| Key | A amount | B amount | Expected selected-row result |
| --- | --- | --- | --- |
| 1 | 3.00 | 3 | IDENTICAL after decimal normalization |
| 2 | -1.25 | -1.20 | CHANGED |

Expected row counts: IDENTICAL=1, CHANGED=1, ONLY_A=0, ONLY_B=0.
For the synthetic account in USD, A totals 1.75, B totals 1.80, and B-minus-A is 0.05.

The expected results follow directly from the synthetic fixture.

## Extended CLI reference

**Availability:** these commands specify the Extended CLI interface for a separately supplied compatible executable. No production binary is currently published in FastDiff-2, and this documentation release does not execute one. See [release status](../RELEASE_NOTES.md).

From the repository root:

```powershell
.\fastdiff-extended.exe extended compare --config .\examples\ledger\ledger.json --out .\ledger-run-01
.\fastdiff-extended.exe extended verify .\ledger-run-01
```

The intended compare status for this fixture is 1 (differences); successful replay returns 0.

For an externally anchored replay, substitute the trusted hash retained at comparison time:

```powershell
.\fastdiff-extended.exe extended verify --manifest-sha256 TRUSTED_HASH .\ledger-run-01
```

To limit row-difference output after full input validation and sorting:

```powershell
.\fastdiff-extended.exe extended ci --config .\examples\ledger\ledger.json --out .\ledger-ci-01 --first-difference
```

Every output directory must be new. Result bundles may contain source data and paths; keep them private.
