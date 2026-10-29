# minija — recipe sharing site

A small static recipe site for friends and family.

- **Live site:** https://skp64-pvt01.github.io/minija-web/
- **Published output:** `skp64-pvt01/minija-web` (written by Publii — do not edit by hand)
- **This repo:** `skp64-pvt01/minija-web-dev` — instructions and configuration notes

The site is authored in [Publii](https://getpublii.com) with the free
[Taste](https://marketplace.getpublii.com/themes/taste/) theme, then published to GitHub Pages
with one **Sync** click. There is no build step, no CI and no server.

## Read in this order

| # | Document | For |
|---|----------|-----|
| 1 | [docs/01-install-publii.md](docs/01-install-publii.md) | Installing Publii and creating the site (once) |
| 2 | [docs/02-theme-and-settings.md](docs/02-theme-and-settings.md) | Theme, URLs, menus, tags, search (once) |
| 3 | [docs/03-github-pages.md](docs/03-github-pages.md) | Publishing to GitHub Pages (once, then whenever the token expires) |
| 4 | [docs/04-adding-a-recipe.md](docs/04-adding-a-recipe.md) | **Every day** — adding and publishing a recipe |
| 5 | [docs/05-backup-and-maintenance.md](docs/05-backup-and-maintenance.md) | Backups, restore, updates, fixes |

Future plans (structured recipe data, cooklang, Hugo) are recorded in [PLAN.md](PLAN.md), not
built yet.

## The one thing to remember

Recipe content lives in the Publii app on the author's laptop, **not in this repo**. If that
laptop dies without a backup, the recipes are gone. See
[docs/05-backup-and-maintenance.md](docs/05-backup-and-maintenance.md).
