# DMC-900H Reference — Android app

A small Android app that shows `DMC900H_VX1005_reference.html` full-screen, offline, and keeps
itself up to date from this repository.

- **The app** carries a copy of the reference from when it was built, so it works with no signal.
- **Updates**: each time the app opens (and when you come back to it after 10 minutes) it asks
  GitHub whether `DMC900H_VX1005_reference.html` in this repo has changed. If it has, it downloads it,
  checks it arrived whole, and offers to reload. If there's no connection, it keeps the last good copy.
- **Rebuilding** is only needed if the app itself changes (the files under `app/`). Uploading a new
  HTML does not trigger a build.

## Updating the reference

1. In this repo: **Add file → Upload files**.
2. Drag in the new `DMC900H_VX1005_reference.html`. It must keep exactly that name.
3. **Commit changes**.

The phone picks it up the next time the app opens. GitHub's file server caches for up to about
5 minutes, so an update made seconds ago may not show until then.

## Opening it in a browser

- The HTML file on its own still opens in any browser, as before.
- Optional: **Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` /
  `(root)` → Save**. After a minute the reference is live at
  `https://<your-username>.github.io/<repo-name>/`, always the latest version you uploaded.

## What's in here

| Path | What it is |
| --- | --- |
| `DMC900H_VX1005_reference.html` | The reference. The only file you normally touch. |
| `index.html` | Redirect so the GitHub Pages address opens the reference. |
| `app/src/main/java/.../MainActivity.java` | The app: WebView, back button, outside links, the update check. |
| `app/src/main/res/` | Icon (an end mill) and the light/dark window colours. |
| `app/build.gradle`, `build.gradle`, `settings.gradle` | Android build settings. |
| `.github/workflows/build.yml` | Builds the signed APK on GitHub and publishes it under **Releases**. |

## Signing

Android only accepts an update to an installed app if it's signed with the same key. That key is
held in the repo's secrets (`SIGNING_KEY`, `SIGNING_PASSWORD`), never in the files. Keep the
`dmc900h-release.jks` backup somewhere safe. If it's lost, the app still works, but a future rebuild
would mean uninstalling and reinstalling instead of updating in place.
