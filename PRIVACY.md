# Privacy and data handling

FastDiff's documented local workflow processes inputs on the operator's machine. Local-file comparison and offline replay do not require sending datasets to the maintainer.

Optional HTTP/GraphQL acquisition contacts endpoints chosen by the operator and is not an offline operation. Endpoint operators may receive request metadata and authorization supplied for those requests.

The local design does not require telemetry, device fingerprinting or online activation. This describes the documented product design, not a certification of an unreleased executable.

## Data retained by a comparison

Result bundles may retain raw snapshots, normalized records, selected fields, source configuration, local paths and difference reports. Spill files and incomplete results may remain after a crash. Treat these artifacts as sensitive when inputs are sensitive.

- Keep credentials out of configuration files, query literals, filenames and public issues.
- Use the supported environment-variable mechanism for connector bearer tokens.
- Apply your own access controls, retention policy and authorized deletion process.
- Do not upload real comparison bundles to this repository.
- Hashes and offline verification do not anonymize data.

The examples in this repository are synthetic. No customer datasets or production license files are distributed here.

Visiting or interacting with this GitHub repository is subject to GitHub's own platform privacy practices.
