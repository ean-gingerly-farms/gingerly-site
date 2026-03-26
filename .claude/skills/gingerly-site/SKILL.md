---
name: gingerly-site
description: "Use this skill for ANY work on the Gingerly Farms website. This includes: editing page content, adding new pages or field notes, updating styles, fixing bugs, changing copy, adding images, modifying navigation, updating SEO/meta tags, or any task that touches HTML/CSS files in this project. Trigger whenever the user mentions the farm site, any page name (index, about, produce, field-notes, contact, find-us), or asks to update/change/add/fix anything on the site. Also trigger when the user discusses voice, tone, or copy direction for the site."
---

# Gingerly Farms Site Updates

## First: Read the Project Memory

Before doing anything, read `CLAUDE.md` in the project root. It contains:
- Voice and tone guidelines (critical for any copy work)
- Site architecture and file structure
- Design system conventions
- SEO checklist for new pages
- Preferences and conventions (no em dashes, email address, etc.)

```
Read CLAUDE.md
```

This is non-negotiable. The voice/tone section has been carefully calibrated through multiple rounds of feedback and is the most important thing to get right.

---

## How This Site Works

Static HTML, no build step, deployed on Netlify. All site files live in the `ui/` folder (the Netlify publish directory). Project-level files (CLAUDE.md, references, .claude/) stay in the repo root.

Each page is a standalone `.html` file that imports shared CSS from `ui/design-system/`. Nav and footer are loaded as HTML partials via JavaScript `fetch()`.

**Always work in `ui/` when editing site files.**

### To edit existing page content:
1. Read `CLAUDE.md` for voice/tone
2. Edit the HTML file in `ui/`
3. Update meta description if the page summary changed
4. Update JSON-LD structured data if relevant fields changed
5. Check for em dashes (not allowed)

### To add a new Field Note article:
1. Read `CLAUDE.md` for voice/tone
2. Copy structure from an existing article (`ui/field-notes/how-we-grow.html`)
3. Create the HTML file in `ui/field-notes/`
4. Add a card to `ui/field-notes.html` (remove a coming-soon placeholder if replacing one)
5. Add BlogPosting JSON-LD with BreadcrumbList
6. Add full SEO meta tags (title, description, OG, Twitter, GEO)
7. Add to `ui/sitemap.xml`
8. Use existing CSS classes from `ui/design-system/field-notes.css` (don't create new stylesheets for articles)

### To add a new top-level page:
1. Read `CLAUDE.md` for voice/tone
2. Use the section/container pattern: `<section class="section [variant]"><div class="container">...</div></section>`
3. Follow the CSS load order in `<head>` (tokens → typography → buttons → nav → footer → layout → patterns → [page].css)
4. Create a page-specific CSS file in `design-system/` if needed
5. Add JSON-LD + BreadcrumbList
6. Add full SEO meta tags
7. Add to nav.html and footer.html
8. Add to sitemap.xml

### To modify styles:
1. Check `design-system/tokens.css` for existing values before creating new ones
2. Use CSS custom properties, not hardcoded values
3. Follow BEM-ish naming: `.component`, `.component__element`, `.component--modifier`
4. Page-specific styles go in `design-system/[page].css`, not inline

---

## Voice/Tone Quick Reference

Think: **explaining your farm to a friend who asked about it at dinner.**

| Do | Don't |
|----|-------|
| State facts and let readers conclude | Moralize about sustainability |
| Use enough detail to be informative | Oversimplify with throwaway words |
| Sound like you take your work seriously | Sound like you're pitching investors |
| Be conversational and direct | Be nonchalant or too-cool |
| "year-round", "consistent", "how it works" | "sustainable", "mission", "why it matters" |

**No em dashes.** Use commas, periods, colons, or parentheses.

**Email:** Always `contact@gingerlyfarms.com`

---

## Post-Update Checklist

After every change, verify:

1. **Copy matches voice/tone** — Read it out loud. Does it sound like a real person talking to a friend?
2. **Meta descriptions match** — If page content changed, update `<meta name="description">`, OG, and Twitter descriptions
3. **JSON-LD is valid** — Check structured data matches the page content
4. **No em dashes** — Search for `—` in any files you touched
5. **Email is correct** — `contact@gingerlyfarms.com` everywhere
6. **CSS uses tokens** — No hardcoded colors, spacing, or font values
7. **Sitemap updated** — If you added or removed a page
8. **Nav/footer updated** — If navigation structure changed
