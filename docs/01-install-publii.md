# 01 — Install Publii and create the site

Do this once, on the author's laptop. About 15 minutes.

## 1. Download and install

Get Publii from <https://getpublii.com/download/> (current version: 0.48.1).

**Linux** — prefer the `.deb`:

```bash
sudo apt install ./Publii-0.48.1.deb
```

Or run it without installing:

```bash
chmod +x Publii-0.48.1.AppImage
./Publii-0.48.1.AppImage
```

**Windows / macOS** — run the `.exe` / open the `.dmg` and follow the installer.

## 2. Create the website

1. Launch Publii.
2. Click **Add new website** (or **Create your first website**).
3. Enter the site name: **`minija`** — the folder name derives from this, and these docs
   assume it.
4. Author name: the display name that will appear on recipes. You can change it later under
   **Authors**.

## 3. Know where the files are

Everything for the site lives **outside this repo**, by default in:

```
~/Documents/Publii/sites/minija/
├── input/      <- the real content: db.sqlite (posts), themes/, media/
├── output/     <- the generated website, replaced on every sync
└── preview/    <- the local preview copy
```

`app.getPath('documents')/Publii` is Publii's own default, so the path is the same shape on
Windows (`Documents\Publii\...`) and macOS (`~/Documents/Publii/...`).

Two consequences to internalise now:

- **Backups matter more than usual.** Posts are inside `input/db.sqlite`, a binary file. Git
  cannot diff or merge it, and it is not in this repo. See
  [05-backup-and-maintenance.md](05-backup-and-maintenance.md).
- **Do not delete `input/`.** That is the site.

You can move the whole location later under **App settings → Files location → Sites
location**, but do it before adding content, not after.

## Done when

Publii shows the site with an empty post list, and **Preview your site** opens in a browser.
The site is not online yet — that is [03-github-pages.md](03-github-pages.md).

Next: [02-theme-and-settings.md](02-theme-and-settings.md)
