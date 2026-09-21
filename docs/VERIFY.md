# Verify package integrity

Verify that the downloaded documentation matches its published checksums before using it as a reference.

SHA256SUMS.txt lists all tracked package files except itself. Paths are relative to the repository root; hashes refer to exact UTF-8/LF bytes. Preserve line endings when checking a downloaded archive.

On systems with sha256sum:

```sh
sha256sum -c SHA256SUMS.txt
```

PowerShell, from the package root:

```powershell
$failed = $false
Get-Content -LiteralPath .\SHA256SUMS.txt | ForEach-Object {
    $expected, $relative = $_ -split '  ', 2
    $actual = (Get-FileHash -LiteralPath $relative -Algorithm SHA256).Hash.ToLowerInvariant()
    if ($actual -ne $expected) {
        Write-Error "Checksum mismatch: $relative"
        $failed = $true
    }
}
if ($failed) { throw 'Package checksum verification failed.' }
```

Release assets include a documentation ZIP and its separate SHA-256 sidecar. The ZIP contains the same package files as the release commit, without Git history or private build artifacts.

## Verification scope

These checks establish package byte integrity. GitHub-hosted checksums and files share a distribution channel, so publisher authentication requires a separately trusted signature or anchor. Executable testing and result-bundle replay are separate operations; this package contains documentation and synthetic examples.
