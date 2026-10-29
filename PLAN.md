# Recipe Sharing Site — Plan

Repo: `skp64-pvt01/minija-web-dev` (docs + config) → `skp64-pvt01/minija-web` (published output)
Live URL: `https://skp64-pvt01.github.io/minija-web/`

---

## 1. Decision

**Publii 0.48.1 + Taste theme 3.3.0, deployed straight to GitHub Pages from the Publii app.**

- Audience: friends and family, link sharing. No Google-discoverability requirement yet.
- Authoring: one person, one laptop, desktop app.
- Deployment: Publii's built-in **GitHub Pages** server type pushes generated files to the
  `main` branch of `minija-web`. No CI, no npm, no custom theme code.
- v1 is **documentation plus configuration**. Every step is a GUI action at the Publii app, so
  the runbook (`docs/`) is the deliverable; this repo holds instructions, not code.

### Verified facts this plan relies on

| Fact | Source |
|---|---|
| Publii 0.48.1 (build 17565, 2026-10-09), Linux AppImage/.deb/.rpm published | getpublii.com/download |
| Native GitHub Pages target (username/org, repo, branch, token, parallel uploads, API rate limiting) | getpublii.com/docs/server-configuration.html |
| The GitHub deployer commits a delta tree **including deletions** → the target branch is 100 % Publii-owned | `app/back-end/modules/deploy/github-pages.js` (`buildDeltaTree`, `createTreeInChunks`) |
| The docs' "1000 file limit" is stale: trees are chunked at 200 entries, no hard cap | same file, `CHUNK_SIZE = 200` |
| Site data at `<documents>/Publii/sites/<site>/{input,output,preview}`; posts in `input/db.sqlite` | `app/back-end/app.js` (`app.getPath('documents')`, `sitesDir`) |
| Backups are `.tar` archives; restore works on a fresh install | getpublii.com/docs/website-backups.html |
| Taste 3.3.0 (2025-11-04), free unlimited use, demo content is a food blog; needs Publii ≥ 0.46 | marketplace.getpublii.com/themes/taste |
| Static Search plugin free, FlexSearch, needs `supportedFeatures.customSearch` | getpublii.com/docs/static-search.html |
| Per-post custom fields exist (`postConfig` in theme `config.json`); `-override` theme folders survive updates | getpublii.com/dev/theme-settings-api, getpublii.com/docs/overriding-publii-theme.html |
| `minija-web` public, Pages enabled, default branch `main`; `minija-web-dev` has no Pages | GitHub API |

---

## 2. Delivered in v1

```
README.md                      orientation + doc index
docs/01-install-publii.md      install, first website, where files live
docs/02-theme-and-settings.md  Taste, Website URL, site/theme settings, tags, search
docs/03-github-pages.md        token, Pages source, Publii server form, sync, verification
docs/04-adding-a-recipe.md     the author's single page
docs/05-backup-and-maintenance.md   backups, restore, updates, fix table
theme-override/README.md       where future Taste customisation goes (empty today)
.gitignore                     guards against committing site data / tarballs
PLAN.md                        this file
```

---

## 3. Sequence and gates

| Stage | Who | Output | Gate |
|---|---|---|---|
| 1 | Done | Docs in §2 committed | Docs reviewed |
| 2 | Author | Publii installed, site + Taste, Website URL set | Local preview looks right |
| 3 | Author | Token, Pages source, Publii server, first sync | Live URL loads with CSS, images, search index |
| 4 | Maintainer | Verify live site against docs; correct any step that did not match the real UI | Docs match reality |
| 5 | Author | First three recipes, About page, tags tidied | A recipe can be published without reading the docs |

Stage 4 is the correction loop: the runbook is unverified until stages 2–3 have actually run,
because none of it can be exercised without the GUI.

---

## 4. Out of scope for v1 (deliberate, not forgotten)

- No custom theme code, CI, build step, comments, analytics, custom domain.
- No structured recipe data (§6.1), no cooklang (§6.2), no scaling/shopping list/print card.
- No second author, no mobile authoring.

---

## 5. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Content lives in `db.sqlite`, not git | Disk loss = site loss; no diffs/history of posts | Backups to a synced folder each session; tarball at milestones; `docs/05` |
| Branch is Publii-owned | Hand edits to `minija-web` are deleted at the next sync | Stated as a hard rule in `docs/03`; additions via File Manager |
| Token scope from docs, untested | `Test connection` may reject a fine-grained token | Classic `repo`-scope fallback documented |
| Site URL subpath | Missing CSS/images on the live site | Exact URL in `docs/02` + `docs/03`; fix-table entry |
| One machine at a time | Second author collides; `db.sqlite` corruption | Documented in `docs/05`; revisit plan if it happens |
| Docs drift from the UI | Stale runbook | Stage 4 verification |

---

## 6. Future requirements (recorded, not built)

Both items share one root cause: they need recipe content that is **machine-readable**. Publii
stores posts in `db.sqlite` and renders ingredients as free-form blocks, so neither is reachable
by configuration alone. Two exit ramps are recorded instead of pretending Publii grows into them.

### 6.1 Schema.org Recipe / Google rich results

Goal: pages eligible for recipe rich results — `name`, `image`, `recipeIngredient[]`,
`recipeInstructions[]`, `recipeYield`, `prepTime`, `cookTime`, `totalTime`, `author`.

- **Option A — stay on Publii.** Add a `postConfig` block to `theme-override/config.json`
  (`ingredients` textarea, `servings`, `prepTime`, `cookTime`) plus a `post.hbs` override
  emitting `<script type="application/ld+json">`. Constraints: ingredients stay free text
  (one per line, parsed in the template), no scaling, no print card. Google requires the JSON-LD
  to match the visible page, so both must come from the same fields. Precedent for the gap:
  GetPublii/Publii discussion #1400 (requested, not built).
- **Option B — build-time.** Free once content is files (see 6.2): JSON-LD generated from parsed
  `.cook` data, validated in CI.
- **Trigger**: the site becomes public-facing, or recipe cards in search are wanted.
- **Validation**: Google Rich Results Test + schema.org `Recipe` required-property checklist.

### 6.2 Cooklang

Goal: recipes are plain-text `.cook` files (YAML front matter; `@ingredient{qty%unit}`,
`#cookware`, `~timer`, `= Sections`, `>` notes) so a parser can give servings scaling, shopping
lists, timers and generated JSON-LD.

- **Fundamental conflict**: Publii cannot read or write `.cook` files. Cooklang as the
  *authoring format* means replacing Publii with a file-based pipeline — Hugo (or Astro,
  Eleventy) plus a cooklang renderer (CookCLI / `cooklang-rs`), deployed to `minija-web` by
  GitHub Actions. The two-repo split in AGENTS.md survives; only the builder changes.
- **Planned route**: prototype the Hugo-based site when cooklang work starts, with structured
  front matter (`ingredients[]`, `yield`, times) driving both the recipe card and the JSON-LD.
  Authoring then moves to a browser CMS over the repo (e.g. Pages CMS) or direct git.
- **Migration cost then** = recipe conversion + a theme + one workflow file. The docs, the
  two-level tag taxonomy (course/cuisine) and the URL shape carry over.
- **Not done now**: no parallel `.cook` copies, no ingredient syntax to memorise. Ingredient
  style in `docs/04` ("amount first, one per line") is a readability rule, and happens to make
  conversion mechanical — but nothing about v1 depends on it.
- **Trigger**: scaling by servings, shopping lists, cook timers, or per-recipe JSON-LD come up
  as real requests.

---

## 7. Definition of done (v1)

1. `README.md` + five `docs/` files reviewed and committed in `minija-web-dev`.
2. Live site at `https://skp64-pvt01.github.io/minija-web/` with Taste styling, working search,
   tag pages and at least one published recipe.
3. A `.tar` backup restored successfully once (restore proven, not assumed).
4. The author publishes a second recipe using only `docs/04-adding-a-recipe.md`.
5. AGENTS.md records v1 scope and the future requirements.
