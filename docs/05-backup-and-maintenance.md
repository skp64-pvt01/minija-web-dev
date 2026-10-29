# 05 — Backup and maintenance

The only part of this project where losing data is possible. Read it twice.

## Why backups are not optional

Recipes live in `~/Documents/Publii/sites/minija/input/` — `db.sqlite` plus `media/`. That
folder is on one laptop and **is not in git**, because a binary database cannot be diffed or
merged. The published site on GitHub contains only the *rendered* HTML: it cannot be re-imported
into Publii as posts.

So: no backup, no recipes.

## 1. Back up (every publishing session)

1. **Tools → Backups → Create backup**. It produces a `.tar` archive of the whole site.
2. Set **App settings → Files location → Backup location** to a cloud-synced folder
   (Dropbox / Drive / OneDrive) so a disk failure is also covered.
3. Keep the last few; delete older ones once the site is live and verified.

Cadence: after each session where you added recipes, and **always before** updating Publii or
the theme.

### Do backups go in this git repo?

By default, **no.** A `.tar` includes every image, so it grows to hundreds of MB and every
commit stores a new copy — git becomes slow and useless. This repo holds instructions and theme
customisations; the *backup* belongs in cloud storage.

Exception: at milestones (site launch, before a major change), you may commit a single tarball
if it is small; `*.tar` is gitignored, so it needs `git add -f`. If you find yourself doing
that regularly, move the backups to a separate object store instead.

## 2. Restore (prove this once, before you need it)

1. Publii → **Add new website** → **Install from backup** tab.
2. Drop the `.tar`, choose the site name, **Create website**.
3. Reinstall the theme plugins the site used (**Tools & Plugins**), then re-enter the **Server**
   token from [03-github-pages.md](03-github-pages.md).

Test the whole path once after the first successful deploy. A restore you have never tried is a
guess.

## 3. Two machines

Publii is single-writer: the site folder must live on one machine at a time. The supported
workaround is to put the **Sites location** in a synced folder and edit from one computer at a
time — never two at once, or `db.sqlite` will be corrupted or one side's posts lost. If a second
person starts publishing, that is the trigger to revisit the plan in [../PLAN.md](../PLAN.md),
not to sync harder.

## 4. Updates

| What | How | Risk |
|---|---|---|
| Publii | Notification in-app, or download the newer build | Back up first. Keep ≤ the latest stable; skipping many versions is fine. |
| Taste theme | Marketplace → new zip → upload | Theme settings persist. `taste-override/` (if it exists) survives updates. |
| GitHub token | Expires (90 days) | Sync starts failing with 401 → issue a new token, re-enter in **Server**. |

Theme customisations belong in `../theme-override/`, never in the theme's own files — updates
overwrite those.

## 5. Fix table

| Symptom | Cause | Fix |
|---|---|---|
| Live site has no CSS or images | Website URL missing the `/minija-web` subpath | **Server → Website URL** = `https://skp64-pvt01.github.io/minija-web`, re-sync |
| Sync fails, "token or server address invalid" | Token expired or wrong repo scope | New token with **Contents: Read and write** on `minija-web` |
| Sync fails, "branch does not exist" | Branch field is `master`/`gh-pages` | Set branch to `main` — and never let a sync run against a branch holding work you care about |
| Deleted post still online | Deletion is not a sync | Sync again |
| Synced, but live site unchanged | Pages build queued (~1 min) | Check the commit list; orange dot = queued |
| Hand-added file on `minija-web` disappeared | Publii owns that branch and deletes unknown files | Re-add it via Publii **File Manager** |
| Search returns nothing | Static Search plugin disabled, or theme search option off | Tools & Plugins → Static Search; Theme → Custom settings → Search |
| Post shows in preview, not on the live site | Saved as draft, or not synced | Publish, then sync |
| Every image is rejected: "…is not a valid supported image. Choose a JPG, PNG…" even for a normal JPG | The **Sharp** resize engine crashes when decoding images on some Linux/Electron builds, so Publii reports a format error that is not true | **App settings → Image resize engine → Jimp → Save settings**, then retry the upload |

### If images keep failing

The message above is spurious — the file is fine. Confirm it by watching the terminal where Publii was
started: `[SharpElectronLinux] Warning: Binaries provided by Electron...` followed by no further output
means the image worker died.

The fix is the setting Publii's own note describes: **App settings → Image resize engine → Jimp**.

- Jimp is pure JavaScript: slower per image, but it does not crash. On a 12-megapixel photo it is a
  second or two — irrelevant for a recipe site.
- The engine can also be set by editing `~/Documents/Publii/config/app-config.json` while Publii is
  closed: `"resizeEngine": "jimp"`.
- Switching engines does not touch existing images; only new uploads use it.
- Leave **Convert images to WebP** off while on Jimp unless you want the wasm encoder involved.

## 6. What this setup cannot do (known, accepted)

- No Schema.org Recipe markup, so no Google recipe rich results.
- No cooklang, no ingredient scaling, no shopping list, no print card.
- One author, one machine, desktop only.
- Custom domain, comments, analytics: not configured.

All four are deliberate for v1 and are recorded, with the migration routes, in
[../PLAN.md](../PLAN.md) §6.
