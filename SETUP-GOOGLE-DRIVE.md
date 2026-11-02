# Hadish Works Manager v4 — Google Drive backup setup

## Before using real business data

1. Host these files over HTTPS (e.g., GitHub Pages). Do not open `index.html` as a `file://` URL.
2. In [Google Cloud Console](https://console.cloud.google.com/), create or choose a project.
3. Enable **Google Drive API** for the project.
4. Configure the OAuth consent screen / Google Auth Platform. Add your own Google account as a test user if the app is in Testing mode. Configure the `drive.appdata` scope. Follow Google's current consent and verification requirements.
5. Create an OAuth client of type **Web application**. Under **Authorized JavaScript origins**, enter the exact site origin, such as `https://YOURNAME.github.io` (no repository path). Add localhost origin if testing locally. You do not need a client secret in this browser app.
6. Copy the **Client ID** ending in `.apps.googleusercontent.com` into the app's **Settings → Google Drive → Save Client ID**.
7. Select **Connect Google Drive** and authorize access. Select **Back up now**. Confirm the app reports a successful cloud backup, then select **Browse / Restore** and confirm the snapshot is listed.
8. Export a JSON backup and store an independent copy outside this device. Test restore with disposable data before relying on it.

## Important limitations

- Cloud backups are **append-only** JSON snapshots in the private Google Drive `appDataFolder` (not visible as ordinary files in My Drive). Old backups are not automatically deleted.
- Cloud backup runs after local edits with a delay **only while the app is open, online, and Google authorization is active**. Browser OAuth tokens expire and you may need to reconnect. This is not a background synchronization service.
- The app keeps local data in `localStorage`, which can be erased by browser settings, app removal, or device issues. Google Drive is a separate recovery layer.
- **No automatic merge or multi-device sync**. Do not edit the same data independently on multiple devices. Restore always requires explicit confirmation and downloads a local safety copy first.
- Google Drive storage and Google account availability are outside the app's control. For stronger protection, keep separate downloaded JSON copies as well.
- No guarantee of zero data loss: check the last successful backup before changing devices or clearing app data.
- Never publish an OAuth client secret or API key in this app. The OAuth Client ID is not a secret.
