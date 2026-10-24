# QSO Graph Desktop updates

The update feed for [QSO Graph Desktop](https://github.com/qso-graph/qso-graph-desktop), served
by GitHub Pages at **https://updates.qso-graph.io/desktop.json**.

Every installed copy with **Check for updates** on asks for that one file, at most once a day, to
learn whether a newer version is out. Nothing about the operator is sent with the request. The
address is all the application knows: where it is served from can change by DNS without a release.

## desktop.json

```json
{
  "format": "qso-graph-desktop-updates",
  "version": 1,
  "stable": { "version": "0.1.0", "files": {
    "win-x64":      { "name": "qso-graph-desktop-0.1.0-win-x64.exe",           "url": "https://github.com/qso-graph/qso-graph-desktop/releases/download/v0.1.0/…", "sha256": "…" },
    "linux-x86_64": { "name": "qso-graph-desktop-0.1.0-linux-x86_64.AppImage", "url": "…", "sha256": "…" },
    "linux-arm64":  { "name": "qso-graph-desktop-0.1.0-linux-arm64.AppImage",  "url": "…", "sha256": "…" },
    "mac-arm64":    { "name": "qso-graph-desktop-0.1.0-mac-arm64.zip",         "url": "…", "sha256": "…" }
  } },
  "early": { "version": "0.2.0", "files": { "…": "…" } }
}
```

- **stable** is offered to everyone on the Stable track; **early** also to those on Early, who are
  offered whichever of the two is newer. `null` offers nothing.
- Each file is the one that installs itself on that platform. The application downloads it only
  from the hosts it carries, and keeps it only if its SHA-256 matches the one here.
- The entry for a release is written by `node scripts/release.mjs feed` in the application's
  repository, from that release's own `SHA256SUMS.txt`.

## How it changes

One commit per change: `early` when a pre-release is published, `stable` when one is promoted.
Each commit is the moment that version was offered, and reverting it withdraws a release. The
format and the steps are in the application's
[docs/RELEASES.md](https://github.com/qso-graph/qso-graph-desktop/blob/develop/docs/RELEASES.md).

`CNAME` names the address GitHub Pages serves this at; `.nojekyll` serves the files as they are.
