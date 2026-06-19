# McKim & Creed Takeoff — Releases

Public distribution point for **McKim & Creed Takeoff**. The app source code lives
in a separate private repo; only the installer and a small version manifest are
published here so the app can self-check for updates.

## Files
- **`version.json`** — the update manifest the app reads on launch:
  ```json
  {
    "version": "1.1.0",
    "installer_url": "https://github.com/McKimCreed/electrical-takeoff-releases/releases/download/v1.1.0/McKimCreedTakeoff-Setup-1.1.0.exe",
    "notes": "What changed in this version.",
    "published": "2026-07-01"
  }
  ```
  The app compares `version` to its own build version; if newer, it shows an
  "update available" banner and can download + run `installer_url`.

## Publishing a new version
1. Build the app exe and the Inno Setup installer in the private repo:
   `ISCC.exe /DAppVersion=X.Y.Z installer\McKimCreedTakeoff.iss`
2. Create a GitHub release here tagged `vX.Y.Z` and attach
   `McKimCreedTakeoff-Setup-X.Y.Z.exe`:
   `gh release create vX.Y.Z McKimCreedTakeoff-Setup-X.Y.Z.exe --repo McKimCreed/electrical-takeoff-releases --title "vX.Y.Z" --notes "..."`
3. Update `version.json` (bump `version`, point `installer_url` at the new asset,
   set `notes` + `published`) and commit.

> The installer is currently unsigned, so SentinelOne/EDR may require a one-time
> allowlist entry. Code-signing the installer removes that friction.
