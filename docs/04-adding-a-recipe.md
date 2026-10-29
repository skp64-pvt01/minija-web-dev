# 04 — Adding a recipe

This is the page to keep open while cooking up a new post. Five minutes per recipe.

## 1. Create the post

**Posts** → **Add new post**. If the button offers an editor choice, pick the **Block editor**
(each paragraph, list or image is its own movable block).

## 2. Fill in the sidebar

Click the gear icon (top right) to open post settings:

- **Title** — what the dish is called. No clickbait needed.
- **Featured image** — the one photo that shows on the cards. Guide: at least 1200 px wide,
  JPG, ~85 % quality, under 500 KB. **Always fill in Alt text** ("porotta and beef curry in a
  black bowl") — it is what blind visitors and search engines read.
- **Tags** — one *course* tag (`Main`), optionally one *cuisine* tag (`Kerala`).
- **Slug** — auto-generated from the title; leave it alone.
- **Excerpt** — first one or two sentences, or insert a **read-more** marker where the preview
  should stop.
- **Status** — keep as draft until the recipe is checked.

## 3. Write the body

Use this skeleton every time. It is what makes the site browsable, and it keeps recipes
consistent for the reader.

```markdown
## Ingredients

- 500 g beef, cubed
- 2 onions, sliced
- 1 tbsp ginger-garlic paste
- 1 tsp chilli powder
- Salt to taste

## Method

1. Heat oil in a heavy pan and brown the onions.
2. Add ginger-garlic paste and fry until the raw smell goes.
3. Add the beef, spices and salt; cook until tender.
4. Finish with coconut milk and simmer five minutes.

## Notes

- Pressure cooker: 4 whistles instead of 45 minutes on the stove.
- Keeps 2 days refrigerated; freezes well.
```

Rules of thumb:

- **One ingredient per line**, amount first — the reader scans the list, not the prose.
- **One action per step.** If a step has "and then", it is two steps.
- **Notes** carries substitutions, storage and provenance — not extra method steps.
- Headings: `H2` for the three sections above, `H3` only if a recipe genuinely has parts
  ("For the masala").

## 4. Preview, save, publish

1. **Preview** — check it on a narrow window too; most visitors arrive on a phone.
2. **Save and close**.
3. **Sync your website** (bottom left). This is the step that publishes. Give GitHub a minute.

## 5. Afterwards

- Look at the live page once: images loading, tags linking to the tag page, search finding the
  new title.
- Fix a typo? Edit, save, sync again — the update is incremental, so it is quick.

## Housekeeping

- Two recipes on the same dish are fine — name them distinctly ("Amma's porotta",
  "Porotta, weeknight version") rather than overwriting.
- Move a post you no longer want off the site with **Move to trash** *and then sync*; otherwise
  the live copy stays up.
- Unsplash/stock photos: add the credit in the post's **Featured image → Credits** field.
