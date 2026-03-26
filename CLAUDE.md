# Gingerly Farms — Project Memory

> This file is read automatically by Claude at the start of every session.
> It serves as persistent memory so new sessions don't start from scratch.

---

## Who We Are

**Gingerly Farms** is a hydroponic farm in Charleston, SC founded by **Ean Lawrence** and **Fulton**. Two Lowcountry guys building a farm. The site exists for **credibility**, not sales. We are not a brand trying to sell a lifestyle. We're two grounded people growing food and building a business.

**Contact email:** contact@gingerlyfarms.com (Google Group)

**Future plans (not on the site yet):** Ginger beer, oysters, crab. These are on the roadmap but we're not ready to talk about them publicly.

---

## Voice & Tone — This Is Critical

The voice of this site is the single most important thing to get right. Every piece of copy should sound like **two guys explaining their farm to a friend who genuinely asked about it over dinner.** Interested, knowledgeable, and real.

### The balance:
- **Not salesy.** Never pitch, never oversell, never use marketing language.
- **Not preachy.** Never lecture about sustainability or the environment. We're not tree huggers on a mission. If something is good for the environment, state it as a fact, don't moralize about it.
- **Not too casual.** Don't try to sound cool or nonchalant. Don't undersell the work or use throwaway language like "stuff" or "just a thing we do." We take this seriously.
- **Respect the reader's intelligence.** Give enough detail to be informative. Don't dumb things down, don't over-explain.

### Good examples:
- "We grow leafy greens and herbs without soil. The plants sit in nutrient-rich water that gets mixed, checked, and recirculated."
- "Short supply chain, fresh product. Fewer miles between the grow room and the plate, and that shows up in the quality."
- "We don't have it all figured out. We're two guys building this one system at a time, learning as we go."

### Bad examples (too salesy):
- "We're building the infrastructure for a sustainable local food system."
- "Our tender and vibrant greens are picked young and delivered fast."
- "Sustainability First" as a heading.

### Bad examples (too casual):
- "Here's the water thing." / "It's basically chemistry homework."
- "Hit us up." / "Stuff we've picked up."
- "Nothing revolutionary, just fewer miles."

### Words to prefer:
- "year-round" over "sustainable" in visible copy (keep "sustainable" in meta/SEO tags)
- "consistent" over "reliable supply chain"
- "how it works" over "why it matters"
- State facts, let readers draw their own conclusions

---

## Site Architecture

**Type:** Static HTML site. No framework, no build step, no bundler. Every page is a standalone `.html` file.

**Deployment:** Netlify. Publish directory is `ui/`.

### File structure:
```
gingerly-site/
├── CLAUDE.md               # Project memory (this file, read by Claude automatically)
├── CODEBASE-ANALYSIS-FOR-GINGERLY-FARMS.md  # Olytics reference (don't modify)
├── .claude/skills/         # Claude skills for this project
├── ui/                     # ← Netlify publish directory (all deployable site files)
│   ├── index.html              # Homepage
│   ├── about.html              # Founders / Our Story
│   ├── produce.html            # What We Grow
│   ├── find-us.html            # Where to Find Us
│   ├── contact.html            # Contact form
│   ├── field-notes.html        # Field Notes index (blog-like)
│   ├── field-notes/
│   │   ├── how-we-grow.html    # Article: How We Grow
│   │   └── why-water-matters.html  # Article: How We Use Water
│   ├── privacy.html
│   ├── terms.html
│   ├── robots.txt
│   ├── sitemap.xml
│   ├── assets/
│   │   └── images/
│   └── design-system/
│       ├── tokens.css          # All design tokens (colors, spacing, type, etc.)
│       ├── typography.css
│       ├── buttons.css
│       ├── nav.css / nav.html  # Shared navigation (loaded via JS partial)
│       ├── footer.css / footer.html  # Shared footer (loaded via JS partial)
│       ├── layout.css          # Section/container primitives
│       ├── patterns.css        # Geo pattern overlays (topo, waves, dots, etc.)
│       ├── home.css            # Homepage-specific styles
│       ├── field-notes.css     # Field Notes styles (Olytics-inspired)
│       └── [page].css          # Other page-specific styles
```

**Important:** All site files live in `ui/`. Project-level files (CLAUDE.md, references, .claude/) stay in the repo root. When editing the site, always work in `ui/`.

### Key patterns:
- **CSS load order:** tokens → typography → buttons → nav → footer → layout → patterns → [page].css
- **Section/Container:** Every content block is `<section class="section [variant]"><div class="container">...</div></section>`
- **Background variants:** `section--white`, `section--surface`, `section--dark`, `section--ocean`
- **On-dark helper:** Add `on-dark` class for white text sections
- **Geo patterns:** Add `pattern-topo`, `pattern-waves`, `pattern-dots`, etc. as classes. Use default (faint) or `-bold` variant.
- **Nav/Footer:** Loaded as HTML partials via `fetch()`. Active link detected by JS matching `window.location.pathname`.
- **Naming:** BEM-ish: `.component`, `.component__element`, `.component--modifier`
- **Design tokens:** All colors, spacing, fonts defined in `tokens.css` as CSS custom properties

### Key colors (from tokens.css):
- `--color-deep: #1A2F38` (dark navy)
- `--color-ocean: #3A5C6F` (ocean blue)
- `--color-sage: #7FAE9B` (coastal sage green)
- `--color-sand: #F4F1EC` (warm sand)
- `--color-oyster: #D9D7D2` (oyster shell)

---

## SEO / GEO / LLM Optimization

Already implemented across the site:
- **JSON-LD** structured data on every page (LocalBusiness, BlogPosting, CollectionPage, BreadcrumbList, WebSite, etc.)
- **Open Graph** and **Twitter Card** meta tags with image dimensions
- **GEO meta tags:** `geo.region=US-SC`, `geo.placename=Charleston`
- **robots.txt** explicitly allows LLM crawlers (GPTBot, Claude-Web, Anthropic-AI, PerplexityBot, Google-Extended, Cohere-AI)
- **sitemap.xml** with all pages and priorities

### When adding a new page, always include:
1. `<title>`, `<meta name="description">`, canonical URL
2. Open Graph tags (og:title, og:description, og:image with dimensions)
3. Twitter Card tags
4. GEO meta tags
5. JSON-LD structured data (appropriate type + BreadcrumbList)
6. Add to `sitemap.xml`
7. Add to nav.html and footer.html if appropriate

---

## Field Notes Section

Styled after Olyticsolutions.com/insights. Text-forward, editorial design. No images on cards.

- **Dark hero banner** with topo pattern overlay
- **Text-only cards** with colored top border (`border-top: 3px solid var(--color-sage)`)
- **Coming soon cards** are greyed out (`fn-card--soon`, opacity 0.45)
- **Article pages** have breadcrumb trail, subtitle, meta line (author / read time / date), and stat blocks
- **Stat blocks:** Dark background, 3-column grid with big numbers and labels

### Current articles:
- **How We Grow** — Our hydroponic process (Our Process tag)
- **How We Use Water** — Water usage in our system (How It Works tag)

### Coming soon placeholders:
- Choosing the Right Cultivars (Growing)
- From Garage to First Sale (Business)
- Growing in the Lowcountry (Charleston)
- Dialing In Nutrients (The Details)

---

## Preferences & Conventions

- **No em dashes** anywhere in visible copy. Use commas, periods, colons, or parentheses instead.
- **No emojis** unless explicitly asked.
- **"sustainable"** — avoid in visible copy; fine in meta tags and JSON-LD keywords for SEO.
- **Email:** Always `contact@gingerlyfarms.com`, never `ean@gingerlyfarms.com`.
- Keep the Olytics-inspired codebase analysis file (`CODEBASE-ANALYSIS-FOR-GINGERLY-FARMS.md`) as a reference but don't modify it.

---

## Update Checklist

When making changes to the site, follow this checklist:

- [ ] Does new copy match the voice/tone guidelines above?
- [ ] Are meta descriptions updated to match any content changes?
- [ ] Is JSON-LD structured data updated/added?
- [ ] Is `sitemap.xml` updated if pages were added?
- [ ] Are nav.html and footer.html updated if navigation changed?
- [ ] No em dashes in visible copy?
- [ ] Email references use contact@gingerlyfarms.com?
- [ ] CSS uses existing design tokens (not hardcoded values)?

---

*Last updated: March 2026*
