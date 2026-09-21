# Verify the documentation package

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

Checksums establish byte integrity only. GitHub-hosted checksums and files share a distribution channel; they are not an independent publisher signature. These checks do not test a FastDiff executable.
