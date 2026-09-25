# Groundwork

Habit tracker + task focus timer, published as a private Claude artifact.

**Live:** https://claude.ai/code/artifact/44836f7b-0c38-41be-9d02-43ed79cb8c22

## Files

| file | role |
|---|---|
| `groundwork.html` | **the source.** Artifact source form — no `<!doctype>`/`<html>`/`<head>`/`<body>`; the publish step adds those. Edit this. |
| `index.html` | generated preview wrapper. Disposable — regenerate with the command below. |

## Updating

Republish `groundwork.html` to the same URL (pass the URL so it updates in place
rather than creating a second artifact). Re-read the live version first — the app
publishes new versions by itself whenever data is saved.

## Careful: `data/tracker.json`

The artifact publishes two files. `data/tracker.json` is **live user data**, written
by the page itself on every check-in — not source, and not in this folder on purpose.
A normal republish of the page carries it over untouched. Never publish a local copy
of it; that would overwrite real history.

## Backups

Settings → **Your data**:

- **Download backup** saves `groundwork-backup-YYYY-MM-DD.json` — every habit, check-in,
  task, layout and setting.
- **Import backup** reads one of those files back in (on this or any other device). It
  asks before replacing anything, and keeps the replaced data in this browser's
  localStorage under `day-rings-v1:before-import`, just in case.

## Layout

Today → **Layout** opens the arranger. *Auto* is the default (rows fill left to right,
as many as fit). *Custom grid* lets you pick columns × rows, then drag habits from the
tray onto spots — or tap a habit, then tap a spot. Empty spots stay empty on Today.
Habits left in the tray show under the board, and new habits drop into the first free
spot. Grouping by category takes precedence over the custom board while it is on.

## Sync across devices (Firebase + GitHub sign-in)

The artifact already syncs through your claude.ai account. The Firebase option is for
a copy you host yourself (e.g. GitHub Pages) — inside the Claude artifact the sandbox
will most likely block the Firebase scripts and the GitHub sign-in popup.

It stays off until `FIREBASE_CONFIG` in `groundwork.html` is filled in. To set it up:

1. **Create a project** at https://console.firebase.google.com.
2. **Authentication → Get started → Sign-in method → GitHub → Enable.** Copy the
   callback URL it shows (`https://<project>.firebaseapp.com/__/auth/handler`).
3. **GitHub → Settings → Developer settings → OAuth Apps → New OAuth App.** Homepage URL:
   where you'll host it. Authorization callback URL: the one from step 2. Paste the
   app's Client ID and a new Client secret back into Firebase's GitHub provider → Save.
4. **Firestore Database → Create database** (production mode), then set these rules
   so each account can only touch its own document:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{uid} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```

5. **Project settings → Your apps → Web (`</>`)** → register an app → copy the
   `firebaseConfig` object into `var FIREBASE_CONFIG = …` near the top of the script.
   (The web config is not a secret; the rules above are what protect the data.)
6. **Authentication → Settings → Authorized domains** → add your host
   (e.g. `jkw2lo.github.io`). `localhost` is there already.
7. **Host it**, e.g. GitHub Pages: repo Settings → Pages → deploy from `main` / root
   (it serves the generated `index.html`).

Then Settings → **Sign in with GitHub**. Each account keeps one document,
`users/{uid}`, holding the whole state; the most recently saved copy wins, and changes
from another device arrive live. Whatever a sync replaces is kept in that browser under
`day-rings-v1:before-sync`.

## Local preview

```
cd "/Users/jenniferlo/Projects/Groundwork" && python3 -m http.server 5191
```

Regenerate the wrapper after editing the source:

```
cd "/Users/jenniferlo/Projects/Groundwork" && { printf '<!doctype html>\n<html lang="en">\n<head>\n<meta charset="utf-8">\n<meta name="viewport" content="width=device-width,initial-scale=1">\n</head>\n<body>\n'; cat groundwork.html; printf '\n</body>\n</html>\n'; } > index.html
```
