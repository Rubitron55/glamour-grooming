# Glamour Grooming — Client Notes

A searchable client + groom-note database for Glamour Grooming, LLC.
1,610 clients are pre-loaded. Your live data lives in **one JSON file that you choose**,
so you can keep it in an iCloud Drive / Dropbox / OneDrive folder and use the same
data on your home computer and your shop computer.

---

## Files in this folder

| File | What it is |
|------|------------|
| `index.html` | The app |
| `seed-data.js` | One-time copy of your existing 1,610 clients (only used until you link a database file) |
| `manifest.webmanifest`, `sw.js`, `icon-*.png` | Make it installable as a desktop app and work offline |

Keep these files together. Don't rename them.

---

## Fastest way to just open it

Double-click `index.html` — it opens in your browser. Use **Chrome** or **Edge**
(Safari and Firefox can't save to a file — see the note at the bottom).

That works, but it opens in a browser tab and doesn't get its own icon. For the
real "desktop app" feel, install it (next section).

---

## Install it as a desktop app (recommended)

An installed app runs in **its own window with its own Dock/taskbar icon — no tabs,
no address bar**. To install, the files need to be served over `https://` once. Easiest
free option is GitHub Pages:

1. Create a free account at <https://github.com>.
2. Make a new repository (e.g. `glamour-grooming`), and upload every file from this
   folder into it.
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a
   branch → Branch: `main` / `root` → Save.**
4. Wait ~1 minute. GitHub shows a URL like
   `https://YOURNAME.github.io/glamour-grooming/`.
5. Open that URL in **Chrome or Edge** on each computer. Click the **Install** icon
   in the address bar (or menu → *Install Glamour Grooming…*). Done — it's now an app
   in your Applications / Start menu.

Updating later: replace the files in the repo, then bump `CACHE = "gg-shell-v1"` to
`"gg-shell-v2"` in `sw.js` so the installed app picks up the new version.

(Netlify, Cloudflare Pages, or any static host works too — they all give you an
`https://` URL you install from.)

---

## Set up the shared database file (do this once)

**On the first computer:**

1. Open the app.
2. Click **"Link database file…"** in the top bar.
3. Choose **Cancel** when asked (that means *"create a new file from my current list"*).
4. In the save dialog, navigate into your **iCloud Drive**, **Dropbox**, or **OneDrive**
   folder and save it as `glamour-grooming.json`.
5. The top bar turns green: *"Saved to glamour-grooming.json"*. From now on every edit
   is written straight to that file.

**On the second computer:**

1. Wait for the cloud folder to finish syncing `glamour-grooming.json` down.
2. Open the app → **"Link database file…"** → choose **OK** (*"open an existing file"*)
   → pick the `glamour-grooming.json` that synced over.
3. Green bar = you're now editing the same file both places.

After that, each computer remembers the file. When a browser asks for permission
again after a restart, click **Reconnect**.

---

## How you know it's actually saving

The green/amber/red bar across the top always tells you the truth:

| Bar | Meaning |
|-----|---------|
| 🟢 **Saved to glamour-grooming.json · 2:16 PM** | Written to your file and read back to confirm |
| 🟡 **Unsaved changes** | You just typed; it saves ~1 second after you stop |
| 🟡 **No database file linked — saving to this browser only** | You haven't linked a file yet |
| 🔴 **Save failed: …** | Something went wrong; a copy was kept in the browser as a fallback |

Edits save automatically when you stop typing, when you click away, and when you press
**⌘S / Ctrl+S**. Every save writes the file, reads it back, and checks the client count
matches before it shows green.

If the file was changed on the *other* computer, this one notices when you switch back
to it and reloads — or warns you if you have unsaved edits of your own.

---

## What changed from the original file

- **One source of truth.** The old version scattered edits across three hidden
  browser-storage slots on top of a baked-in list. Now everything is in the JSON file
  you can see, back up, and move.
- **Real, verified saving** with an honest status bar (the old one always said "Saved"
  even when the write failed).
- **Works on two computers** via a synced file.
- **Export backup / Import** buttons — download a timestamped `.json` any time.
- **Archive a client** (soft delete; tick *Show archived* to bring anyone back).
- **Editable "Last groomed" date**, and the "needs grooming" badge now reads the newest
  dated line in the notes automatically.
- Installable as a standalone app; works offline once hosted.

---

## Backups

Even with the synced file, click **Export backup** now and then — it downloads
`glamour-grooming-backup-YYYY-MM-DD.json`. To restore or move data, use **Import…**.

---

## Browser note

The save-to-file feature needs the **File System Access API**, which today means
**Chrome or Edge** (desktop). In Safari or Firefox the app still runs and you can edit,
but you must use **Export / Import** to move data — it won't write the file directly.
