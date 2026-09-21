# Privacy and data handling

FastDiff's local workflow keeps comparison inputs and retained evidence under the operator's control. Local-file comparison and offline replay process data on the operator's machine, without sending datasets to the maintainer.

Optional HTTP/GraphQL acquisition is the network stage and contacts endpoints chosen by the operator. Endpoint operators may receive request metadata and authorization supplied for those requests.

Local operation is designed to work without telemetry, device fingerprinting or online activation. This page describes the documented architecture; executable release status is tracked in [RELEASE_NOTES.md](RELEASE_NOTES.md).

## Data retained by a comparison

Result bundles may retain raw snapshots, normalized records, selected fields, source configuration, local paths and difference reports. Spill files and incomplete results may remain after a crash. Treat these artifacts as sensitive when inputs are sensitive.

- Keep credentials out of configuration files, query literals, filenames and public issues.
- Use the supported environment-variable mechanism for connector bearer tokens.
- Apply your own access controls, retention policy and authorized deletion process.
- Do not upload real comparison bundles to this repository.
- Hashes and offline verification do not anonymize data.

The examples in this repository are synthetic. No customer datasets or production license files are distributed here.

Visiting or interacting with this GitHub repository is subject to GitHub's own platform privacy practices.
