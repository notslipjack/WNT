# WNT TSM 3.0

Single-file vanilla JS toolkit for TSM / TSE work. Open the `.htm` in a browser. No server required.

Current file: `WNT-TSM-3.0_31AUG2026-32.htm`

Older dated copies in this folder are snapshots. Use the highest generation number.

## What you get

- Module tiles, Custom category, search, themes (including Catppuccin and seasonal canvases)
- Environment URLs and Okta / SSO launch helpers
- New-hire roster and Progress Board (shared roster helpers)
- Outlook-style calendar (`.ics` / classic CSV in, JSON backup in WNT)
- ctxt.io share pad, Linux field guide, TSE networking pack
- Options in one dialog: theme on top, Custom + Reset, then export / import / stats
- Plasma background (4rknova 2016). Use theme colors maps A-D to `--bg-deep`, `--bg-panel`, `--bg-panel-2`, `--border-subtle`

## JSON exports (required)

Every data export is UTF-8 `application/json` with a `.json` filename. Settings, auto-backup, new-hire packages, knowledge, links.

Envelope:

```json
{
  "format": "wnt_export",
  "format_version": 2,
  "kind": "settings",
  "data": {}
}
```

Import accepts v2 envelopes and older flat JSON. Saving a local copy of the app itself stays `.htm`.

## Android wrapper

Folder: `WNT-Android-Wrapper`  
Zip: `WNT-Android-Wrapper.zip`

There is no prebuilt APK in this tree (no Android SDK on the machine that packed it). Open the folder in Android Studio and **Build > Build Bundle(s) / APK(s) > Build APK(s)**.

| Field | Value |
| --- | --- |
| App name | WNT |
| Package | `com.nocarbon.wnt` |
| versionName | 3.0.2 |
| versionCode | 3 |

Toolbar: Open WNT file (SAF picker), Load bundled copy (`assets/wnt.htm`), Update.

http(s) links leave the WebView and open in the real browser so Okta / ServiceNow cookies stay in a normal session.

html2app.dev wants a zip with `index.html` at the root. Use `wnt-html2app.zip`, not the dated `.htm` and not the Android project zip. Save App Metadata before you upload or that site blocks the drop zone.

## Hands-off APK updates

The phone cannot read a private GitHub repo. Source can be private. The update feed must be public.

Public repo in use: https://github.com/notslipjack/WNT/

If that repo is private, raw update.json and release APKs 404 for everyone else. Make it public, or keep source private and publish only the JSON plus WNT.apk on a public repo.

1. Put update.json on the default branch (main or master).
2. Copy .github/workflows/publish-update.yml from the wrapper onto that repo.
3. Settings > Actions > General > Workflow permissions > Read and write.
4. Wrapper is baked to check:

```
https://raw.githubusercontent.com/notslipjack/WNT/main/update.json
```

If the default branch is master, change main to master.

5. Each ship: bump versionCode in app/build.gradle, build WNT.apk, create a Release on notslipjack/WNT, attach that file as WNT.apk, put versionCode: 3 in the release body.
6. The workflow rewrites update.json. The wrapper checks a couple seconds after launch and prompts Update WNT?

update.json for this account:

```json
{
  "versionName": "3.0.1",
  "versionCode": 2,
  "apkUrl": "https://github.com/notslipjack/WNT/releases/download/v3.0.1/WNT.apk",
  "htmUrl": "https://github.com/notslipjack/WNT/releases/download/v3.0.1/WNT-TSM-3.0.htm",
  "notes": "what changed"
}
```

A sample lives at `WNT-Android-Wrapper/update.json`. Android will still ask the user to confirm the install. Sideload cannot silent-replace itself.

Optional private repo (`wnt-source` or similar) is only for you. The APK never fetches it.

## Local conventions

- Dated release notes at the top of `RELEASE_NOTES_HTML` on every meaningful edit
- No em-dashes in shipped code
- Newly Added is derived from `added: "31AUG2026"` on modules, not a drop target
- Custom tiles: long-press on mobile to pin, X on the tile to remove (one-time confirm, then suppress)

## Files in this folder

| File | What it is |
| --- | --- |
| `WNT-TSM-3.0_31AUG2026-32.htm` | Current toolkit |
| `WNT-TSM-3.0_31AUG2026-13.htm` … `-28.htm` | Prior snapshots |
| `WNT-Android-Wrapper/` | Android Studio project |
| `WNT-Android-Wrapper.zip` | Same project, zipped |
| `wnt-html2app.zip` | `index.html` + `config.json` for html2app.dev |
