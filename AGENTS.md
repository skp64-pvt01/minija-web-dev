# Website for Sharing Recipes

- The objective is to develop a simple web-site for publishing recipes.
- The site need to be easy to author and maintain even by those not well versed
  with web development or programming.
- The site should be hosted on Github and published as Github pages.
- A candidate approach is to use the _**[Publii](https://getpublii.com)**_ CMS
  framework with an appropriate Theme / Template.
- For a candidate theme see
  _[Taste Theme](https://marketplace.getpublii.com/themes/taste/)_

## Development

- The development shall use the github repo
  [https://github.com/skp64-pvt01/minija-web-dev.git](https://github.com/skp64-pvt01/minija-web-dev.git)
- The deployment shall use
  [https://github.com/skp64-pvt01/minija-web.git](https://github.com/skp64-pvt01/minija-web.git),
  meaning _Publii_ shall copy / sync the artifacts to this repo.
- Need to produce clear instructions on how to configure _Publii_ and also the
  configuration needed to get the Github pages correctly configured with
  _Publii_ generated artifacts.

## Scope of v1

- v1 is configuration and documentation only: Publii install, Taste theme,
  GitHub Pages deployment, backup routine. No custom theme code, no CI, no
  build step.
- Authoring is single-user and desktop-only (the Publii app on the author's
  laptop). Recipe content lives in Publii's local `db.sqlite`, not in this
  repo; treat backups as the only copy that survives a disk failure.

## Future requirements (explicitly out of scope for v1)

- **Schema.org Recipe / rich results.** Ingredients, yield, prep/cook times and
  image must be exposed as JSON-LD `Recipe` data so pages are eligible for
  Google recipe rich results.
- **Cooklang.** Recipes authored and stored as `.cook` plain text (with YAML
  front matter), rendered to HTML with ingredients, cookware and timers parsed
  — enabling servings scaling, shopping lists and cook timers.

Both need recipe content to be machine-readable. Publii keeps posts in
`db.sqlite`, not files, and renders ingredients as free-form blocks, so neither
is achievable by configuration alone. Do not add features that deepen that
lock-in without revisiting the authoring tool.

Expected route for both: prototype the cooklang support under a Hugo-based
static site (content as `.cook` files, rendering + JSON-LD at build time,
deployed to `minija-web` by GitHub Actions). The two-repo split stays as it is;
only the builder changes. Keep recipes and the tag/course taxonomy portable so
that migration stays a conversion job, not a rewrite.

See `PLAN.md` §6 for the options, tradeoffs and migration triggers.

## Documentation

The setup runbook lives in `docs/` (install, theme/settings, GitHub Pages,
adding a recipe, backup/maintenance). Keep it accurate for a reader who is not
a programmer; when a UI step changes, fix the doc in the same change.
