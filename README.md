# WNT TSM 3.0

Single-file vanilla JS toolkit for TSM / TSE work. Open the `.htm` in a browser. No server required.

Current file: `WNT.htm` - this is the file the Android wrapper actually fetches and displays, and it's kept current with every change. Dated snapshot copies (`WNT-TSM-3.0_DDMMMYYYY-NN.htm`) are point-in-time history, not the live version - if both exist, `WNT.htm` is the one to trust.

## What you get

- Sidebar navigation (collapsible on desktop, slide-in drawer on mobile) with categories, a Custom category you build yourself by dragging tiles onto it, a Newly Added section, global search, and themes (including Catppuccin and seasonal canvases)
- Environment URLs and Okta / SSO launch helpers
- New-hire roster and Progress Board (shared roster helpers)
- Outlook-style calendar (`.ics` / classic CSV in, JSON backup in WNT), now also documents Google Calendar import/export through the same `.ics` files
- ctxt.io share pad, Linux field guide, TSE networking pack
- BIPS Support Escalation Process and The OSI Model reference guides
- Options in one dialog: theme on top, Custom + Reset, then export / import / stats
- Plasma background (4rknova 2016), with a drop shadow under tiles while it's active so they stay readable. Use theme colors maps A-D to `--bg-deep`, `--bg-panel`, `--bg-panel-2`, `--border-subtle`

## JSON exports (required)

Every data export is UTF-8 `application/json` with a `.json` filename. Settings, auto-backup, new-hire packages, knowledge, links.

Envelope:

```
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

| Field       | Value              |
| ----------- | ------------------ |
| App name    | WNT                |
| Package     | `com.nocarbon.wnt` |
| versionName | 3.0.2              |
| versionCode | 3                  |

Toolbar: Open WNT file (SAF picker), Load bundled copy (`assets/wnt.htm`), Update.

http(s) links leave the WebView and open in the real browser so Okta / ServiceNow cookies stay in a normal session.

html2app.dev wants a zip with `index.html` at the root. Use `wnt-html2app.zip`, not the dated `.htm` and not the Android project zip. Save App Metadata before you upload or that site blocks the drop zone.

## Hands-off APK updates

The phone cannot read a private GitHub repo. Source can be private. The update feed must be public.

Public repo in use: <https://github.com/notslipjack/WNT/>

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

A sample update.json lives at `WNT-Android-Wrapper/update.json`. Android will still ask the user to confirm the install. Sideload cannot silent-replace itself.

Optional private repo (`wnt-source` or similar) is only for you. The APK never fetches it.

## Local conventions

- Dated release notes at the top of `RELEASE_NOTES_HTML` on every meaningful edit - append, never rewrite prior entries
- No em-dashes in shipped code
- Newly Added is derived from `added: "DDMMMYYYY"` on modules, not a drop target
- Custom tiles: drag any tile onto the Custom category icon in the sidebar to add it, or drag it back onto All Modules to clear the override; long-press also works on mobile
- New sidebar categories can be reordered by dragging their icons; any tile can be dragged onto a different category icon to recategorize it

## Files in this folder

*(Listing below reflects the structure as of the last confirmed update - worth a quick check against the actual repo before relying on it, since dated snapshots and the Android wrapper assets weren't independently re-verified this pass.)*

| File                                       | What it is                                    |
| ------------------------------------------ | --------------------------------------------- |
| `WNT.htm`                                  | Current, live toolkit - what the wrapper reads |
| `update.json`                              | Version manifest the wrapper polls for updates |
| `WNT-Android-Wrapper/`                     | Android Studio project                        |
| `WNT-Android-Wrapper.zip`                  | Same project, zipped                          |
| `wnt-html2app.zip`                         | `index.html` + `config.json` for html2app.dev |
