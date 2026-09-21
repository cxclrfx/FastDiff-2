# FastDiff V2 documentation

Build a repeatable reconciliation workflow: define identity, acquire and normalize sources, compare large data states, then retain a bundle that can be verified offline.

FastDiff combines exact keyed differences, declared-schema comparison and fixed-point financial reconciliation with external sorting for unsorted inputs. Core handles sorted files; Connectors prepares sources; Extended adds disk-backed sorting and operational comparison modes.

| Your objective | Read |
| --- | --- |
| Understand the system and supported inputs | [Product overview](../README.md) |
| Follow a concrete comparison and replay | [Workflow and synthetic ledger](WORKFLOW.md) |
| Set keys, mappings, resource limits and CI behavior | [Comparison contract](CONTRACT.md) |
| Verify the downloaded documentation package | [Package verification](VERIFY.md) |
| Keep sensitive inputs and bundles local | [Privacy and data handling](../PRIVACY.md) |
| Review operational safeguards or report a vulnerability | [Security](../SECURITY.md) |
| Check component versions and binary availability | [Release notes](../RELEASE_NOTES.md) |
| Understand delivery and licensing | [Licensing](LICENSING.md) |

## Scope / Current release status

The current package contains documentation and synthetic examples. Production binary delivery is pending the release gates in [RELEASE_NOTES.md](../RELEASE_NOTES.md). CLI examples specify the compatible Extended interface; fixture expectations are provided for inspection. Resource ceilings, supported formats and the distinction between replay and independent certification are defined in the [contract](CONTRACT.md).
