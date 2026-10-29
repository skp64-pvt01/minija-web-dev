# 02 — Theme and site settings

Do this once, after [01-install-publii.md](01-install-publii.md). About 20 minutes.

## 1. Install the Taste theme

1. Download the theme zip: <https://marketplace.getpublii.com/themes/taste/> →
   **Download** (`taste_3.3.0.0.zip`). Free, unlimited use.
2. In Publii: **Theme** → **Add new theme** → upload the zip → **Activate**.

Taste is a card-based theme built for food and creative blogs; its own demo is a recipe site.
It requires Publii 0.46 or newer.

## 2. Website URL — the setting that breaks sites

**Server** screen → **Website URL**:

```
https://skp64-pvt01.github.io/minija-web
```

Include the `/minija-web` part. This is a GitHub *project* page, not a user page, so the path is
part of the address. If you type it without the subpath, the live site loads with no CSS and no
images.

- Leave **Use relative URLs** off (Open Graph tags, sitemap and RSS need the absolute URL).
- You can fill this in before configuring the deployment method.

## 3. Site settings

**Site settings** → **General**:

- Website name: `minija` (or the family name you want in the title and footer).
- Tagline / description: one line, e.g. recipes we cook and share.
- Language: your language. Taste ships several.

**Site settings** → **Advanced options** → **SEO**: homepage title and meta description.
Since this site is for friends and family, defaults are fine; do not spend time on SEO here.

## 4. Theme settings

**Theme** → **Basic settings**:

| Setting | Suggested |
|---|---|
| Posts per homepage | 9 |
| Posts per tag page | 12 |
| Excerpt length | 25 words |
| Website logo | optional, SVG or PNG |

**Theme** → **Custom settings**:

- **Layout** — homepage layout (grid vs masonry), number of columns.
- **Post list** — show dates and author avatars or not. Dates are useful for recipes.
- **Colors / Fonts** — Taste ships locally-hosted variable fonts; pick one pair and stop.
- **Menu/Navbar** — mobile menu style (sidebar is default).
- **Footer** — copyright text.

## 5. Menus

**Menus** screen → add a menu, assign it to the main navigation:

- **Home** — the post list.
- **Recipes** — the tags page (Taste generates it) or a hand-made "All recipes" page.
- **About** — a page you create under **Pages**.

## 6. Tags = the recipe taxonomy

**Tags** screen. Keep it to two dimensions so browsing stays useful:

- Course: `Starter`, `Main`, `Dessert`, `Breakfast`, `Drinks`
- Cuisine: `Indian`, `Italian`, `Kerala`, `Baking`, …

Add a one-line description to each tag; it shows on the tag page and is searchable.
Do not use tags as keywords — more than ~25 tags and the tag index becomes noise.

## 7. Enable search

1. **Tools & Plugins** → **Static Search** → enable.
2. In its settings: index post title, excerpt, headings, meta description. Leave the rest.
3. **Theme** → **Custom settings** → **Search** → enable the search field.

Search is generated as a static index and runs in the visitor's browser, so it works on GitHub
Pages with no server. After a sync, confirm it exists at
`https://skp64-pvt01.github.io/minija-web/media/plugins/staticSearch/index.js`.

## Done when

`Preview your site` shows: Taste styling, a search field, an empty post list, working menu
links, and one About page. Screenshot it before moving on — when the live site looks different,
the cause is almost always the Website URL from §2.

Next: [03-github-pages.md](03-github-pages.md)
