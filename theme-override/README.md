# theme-override — future Taste customisations

Empty on purpose. Nothing here is used by the site today.

When a template or CSS change to Taste is genuinely needed, put it here instead of editing
`~/Documents/Publii/sites/minija/input/themes/taste/`, because theme updates overwrite the theme
folder but leave override folders alone.

## How it works

Publii looks for `<theme>-override/` next to the theme and uses any file it finds there in place
of the original, at the same relative path:

```
taste-override/
├── post.hbs                       replaces themes/taste/post.hbs
├── config.json                    add postConfig / customConfig fields
└── assets/css/custom.css          replaces themes/taste/assets/css/custom.css
```

To activate: create `taste-override/` inside `~/Documents/Publii/sites/minija/input/themes/`
and copy this repo's contents into it. Keep this repo as the source of truth and copy outward —
never edit the live override folder as the only copy.

Notes:

- Only override what you must; anything missing falls back to the theme's own file.
- An overridden theme will not show up as "customised" in Publii's theme list.
- An override `.hbs` file must contain at least one character (a blank file breaks generation).

## Why this exists

The only likely first use is a Schema.org `Recipe` JSON-LD block driven by `postConfig` fields —
see [../PLAN.md](../PLAN.md) §6.1. It is not needed until the site is public-facing.
