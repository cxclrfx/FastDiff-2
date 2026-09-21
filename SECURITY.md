# Security

## Supported release scope

This repository distributes the FastDiff V2 system documentation and synthetic examples. Production executable availability, qualification and support scope will be specified with the applicable binary release; see [current release status](RELEASE_NOTES.md). This documentation package carries no executable security certification.

## Report a vulnerability privately

Use the repository's **Security -> Report a vulnerability** feature when available:

[Private vulnerability report](https://github.com/cxclrfx/FastDiff-2/security/advisories/new)

If private reporting is unavailable, open an issue asking the maintainer to establish a private reporting channel. Include no exploit details, credentials, customer data or private files in that issue.

For a private report, provide the affected component/version, a minimal synthetic reproduction, expected and observed behavior, and impact. Remove credentials, license files, real records and machine-specific paths. No response-time commitment is currently published.

## Operational boundaries

- Process only data and endpoints you are authorized to access.
- Treat configuration, mappings and selected keys as part of the comparison contract.
- Retain complete output bundles privately; hashes do not sanitize their contents.
- Keep a trusted manifest hash separately from the bundle.
- Use a new output directory for each comparison. Interrupted output is incomplete.
- Do not disable Windows application control to run a blocked executable.
- SQLite input must be a quiescent, checkpointed export; live WAL/journal capture is outside scope.
- Optional network connectors contact explicitly configured endpoints. Local/offline operation requires local inputs.

Checksums detect changed bytes; they are neither a publisher signature nor proof of correct behavior.
