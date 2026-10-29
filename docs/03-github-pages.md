# 03 — Publishing to GitHub Pages

Do this once, then again only when the token expires. About 10 minutes.

## How it works

Publii generates the site locally, then uses the GitHub API to commit every file to the
`main` branch of `skp64-pvt01/minija-web`, and GitHub Pages serves that branch.

```
Publii (laptop)  --sync-->  minija-web:main  --GitHub Pages-->  https://skp64-pvt01.github.io/minija-web/
```

> **Hard rule: `minija-web:main` belongs to Publii.**
> Every sync replaces the tree and **deletes anything Publii did not generate**. Never hand-edit
> or commit to that branch — not a README, not a file you added "just once". Anything that must
> be on the site (a `CNAME`, a `robots.txt`, a domain-verification file) goes in through
> Publii's **File Manager**, which puts it in `input/files/` and ships it with every sync.

## 1. Create an access token

Use a fine-grained token, limited to the one repository:

1. <https://github.com/settings/personal-access-tokens/new>
2. Token name: `Publii minija-web`. Expiration: 90 days (calendar reminder: renew it).
3. **Repository access** → *Only select repositories* → `skp64-pvt01/minija-web`.
4. **Permissions** → *Repository permissions* → **Contents: Read and write**. Nothing else.
5. Generate, copy the token once, store it in your password manager.

If **Test connection** in step 3 fails with a 401/403 while the repo and branch are correct,
fall back to a classic token — <https://github.com/settings/tokens/new> with the single `repo`
scope — which is what Publii's own guide uses. The deployer only needs contents access, so the
fine-grained token normally works.

Never paste the token into this repo, an issue, a commit message or a chat.

## 2. Point GitHub Pages at the branch

1. <https://github.com/skp64-pvt01/minija-web/settings/pages>
2. **Source**: *Deploy from a branch*.
3. **Branch**: `main`, folder `/ (root)`. **Save**.

Pages is already enabled on this repo; you are only confirming the source.

## 3. Configure Publii

**Server** screen → **Change server type** → **GitHub Pages**:

| Field | Value |
|---|---|
| Website URL | `https://skp64-pvt01.github.io/minija-web` (from doc 02 §2) |
| Use relative URLs | off |
| API server | leave default (`https://api.github.com`) |
| Username/Organization | `skp64-pvt01` |
| Repository | `minija-web` |
| Branch | `main` |
| Token | the token from §1 |
| Parallel uploads | `1` |
| API rate limiting | on |

Click **Test connection** → then **Save settings**.

## 4. First sync

1. **Sync your website** (bottom left of the app).
2. Wait for the progress to finish — the first sync uploads everything.
3. Open <https://skp64-pvt01.github.io/minija-web/>. A 404 for the first ~1 minute is normal:
   GitHub is rebuilding. Check <https://github.com/skp64-pvt01/minija-web/commits/main> —
   orange dot = queued, green tick = deployed.

## 5. Verify the live site

- Page loads **with styling** and images. If it is unstyled HTML, the Website URL is wrong.
- A recipe page opens.
- Search works: `/media/plugins/staticSearch/index.js` returns JavaScript, not a 404.
- The browser tab and social preview show the right title (that comes from the absolute URL).

## Everyday use after this

Edit → **Preview** → **Save** → **Sync your website**. Nothing else. Saving a post does *not*
publish it; only a sync does.

Next: [04-adding-a-recipe.md](04-adding-a-recipe.md)
