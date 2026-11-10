# cable-design-center-updates

Public version manifest for **Cable Design Center** (Blue Robotics).

The application's source and installers live in a private repository. Installed
copies of the app read [`latest.json`](latest.json) from this public repo, a
few seconds after startup and from **Help → Check for Updates…**, to find out
whether a newer version exists. If one does, the app shows a banner with a
**Download** button that opens the release page on GitHub. Nothing is downloaded
or installed automatically, and the app sends nothing beyond a plain HTTPS GET
of this file.

```
https://raw.githubusercontent.com/bluerobotics/cable-design-center-updates/main/latest.json
```

## Don't edit by hand

`latest.json` is written by the release workflow in the main repository each
time a `v*` tag is published, using a fine-grained token that can only write to
this repo. A manual edit will be overwritten by the next release.

## Format

```json
{
  "schemaVersion": 1,
  "version": "0.2.0",
  "tag": "v0.2.0",
  "releaseUrl": "https://github.com/bluerobotics/cable-design-center/releases/tag/v0.2.0",
  "publishedAt": "2026-11-10T18:00:00Z",
  "prerelease": false,
  "notes": "- Short summary of changes",
  "stable": {
    "version": "0.2.0",
    "tag": "v0.2.0",
    "releaseUrl": "https://github.com/bluerobotics/cable-design-center/releases/tag/v0.2.0",
    "publishedAt": "2026-11-10T18:00:00Z",
    "prerelease": false,
    "notes": "- Short summary of changes"
  }
}
```

| Field | Meaning |
| --- | --- |
| `version` | Semantic version of the newest published release (may be a prerelease such as `0.3.0-test.1`). |
| `tag` | Git tag of that release. |
| `releaseUrl` | Release page. The app only opens URLs under `https://github.com/bluerobotics/cable-design-center/releases/`. |
| `publishedAt` | ISO 8601 publish time. |
| `prerelease` | `true` for tags containing `-`. Prereleases are only offered to people already running a prerelease. |
| `notes` | Short plain-text / Markdown summary shown in the banner. |
| `stable` | The newest non-prerelease (same fields), or `null`. Users on a stable version are compared against this entry. |

The release page itself may be in a private repository, in which case only
people with access to it can download the installer.
