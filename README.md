# fxx-releases

Release artifacts for **fxx** (com.fxx.app), an Arabic-first local-first
companion for XAUUSD day traders. This repository holds no source code â€” only
the signed APKs and the update manifest the app's in-app updater fetches.

## The stable endpoint

    https://github.com/amworx/fxx-releases/releases/latest/download/fxx-manifest.json

Every release uploads the manifest under that name, so the URL keeps working as
releases pile up. The manifest describes one release:

    {
      "version":     "1.0.0",
      "versionCode": 16,
      "apkUrl":  "https://github.com/amworx/fxx-releases/releases/download/v16/fxx-1.0.0-16.apk",
      "sha256":     "FFCAF4B3...792E",
      "sizeBytes":  59785106,
      "notes":      "fxx 1.0.0 (16)"
    }

The app compares `versionCode` against the version the package manager says is
installed, downloads the APK named by `apkUrl`, resumes with a Range request
if a download was paused, and refuses to offer an install whose SHA-256 does not
match `sha256` (fail closed). Nothing installs silently â€” Android always asks
the user to approve.

Settings can point at a different manifest URL, which is how a build is tested
before this endpoint is updated.

## Signing

The APKs here are signed with the same debug/self-signed key as the builds
installed on the project's test device, so they upgrade in place. Certificate
SHA-256:

    08f1dec1649f2eb75dcc236914d0843582fd9b056e41f4cda209a576a784a298