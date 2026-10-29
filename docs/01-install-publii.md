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
3. Site icon — pick any; it only labels the site inside the Publii interface and never appears
   on the published website.
4. Interface colour — likewise cosmetic: it tints the app window, not the site.
5. Website name: **`minija`** — the folder name derives from this, and these docs assume it.
   It is also the default text logo and page-title prefix until you change it.
6. Author name: the display name that will appear on recipes. This creates your first author;
   change it later under **Authors**.
7. **Create website**.

### There is no theme choice here

The creation dialog does **not** ask for a theme. Publii gives the new site a built-in default
theme so the preview works, and you pick the real one afterwards —
[Taste, in doc 02 §1](02-theme-and-settings.md#1-install-the-taste-theme). Expect the site to
look plain and unrelated to the final design until then; that is normal, not a mistake.

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

Publii shows the site with an empty post list, and **Preview your site** opens in a browser —
still wearing Publii's default theme, which is expected. The site is not online yet, and Taste
is not installed yet; those are the next two documents.

Next: [02-theme-and-settings.md](02-theme-and-settings.md)
