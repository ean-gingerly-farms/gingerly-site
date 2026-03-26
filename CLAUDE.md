# Gingerly Farms — Project Memory

> This file is read automatically by Claude at the start of every session.
> It serves as persistent memory so new sessions don't start from scratch.

---

## Who We Are

**Gingerly Farms** is a hydroponic farm in Charleston, SC founded by **Ean Lawrence** and **Fulton Williams**. Two Lowcountry guys building a farm. The site exists for **credibility**, not sales. We are not a brand trying to sell a lifestyle. We're two grounded people growing food and building a business.

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

**Domain:** gingerlyfarms.com

**Analytics:** Google Analytics 4, tag ID `G-V69H5SY1FS`

### File structure:
```
gingerly-site/
├── CLAUDE.md                   # Project memory (this file)
├── CODEBASE-ANALYSIS-FOR-GINGERLY-FARMS.md  # Olytics reference (don't modify)
├── .claude/skills/             # Claude skills for this project
├── ui/                         # Netlify publish directory
│   ├── index.html              # Homepage
│   ├── about.html              # Founders / Our Story
│   ├── produce.html            # What We Grow
│   ├── find-us.html            # Partners
│   ├── contact.html            # Contact (mailto, no form backend)
│   ├── field-notes.html        # Field Notes index (blog-like)
│   ├── field-notes/
│   │   ├── how-we-grow.html    # Article: How We Grow
│   │   └── why-water-matters.html  # Article: How We Use Water
│   ├── privacy.html            # Privacy Policy (references GA)
│   ├── terms.html              # Terms of Service
│   ├── 404.html                # Custom 404 page (noindex)
│   ├── robots.txt              # Allows LLM crawlers
│   ├── sitemap.xml             # 10 pages with priorities
│   ├── site.webmanifest        # Web app manifest
│   ├── favicon.ico             # ICO fallback favicon
│   ├── _headers                # Netlify security + cache headers
│   ├── _redirects              # HTTPS, www redirect, clean URLs, 404 catch-all
│   ├── assets/
│   │   └── images/             # All site images (optimized JPG/PNG)
│   └── design-system/
│       ├── tokens.css          # All design tokens (colors, spacing, type)
│       ├── typography.css
│       ├── buttons.css
│       ├── nav.css / nav.html  # Shared navigation (loaded via JS partial)
│       ├── footer.css / footer.html  # Shared footer (loaded via JS partial)
│       ├── layout.css          # Section/container primitives + print styles
│       ├── patterns.css        # Geo pattern overlays (topo, waves, dots, etc.)
│       ├── home.css            # Homepage-specific styles
│       ├── about.css
│       ├── produce.css
│       ├── find-us.css
│       ├── contact.css         # Includes .contact-cta classes for mailto layout
│       ├── field-notes.css     # Field Notes styles (Olytics-inspired)
│       └── legal.css           # Privacy + Terms pages
```

**Important:** All site files live in `ui/`. Project-level files (CLAUDE.md, references, .claude/) stay in the repo root. When editing the site, always work in `ui/`.

### Key patterns:
- **CSS load order:** tokens > typography > buttons > nav > footer > layout > patterns > [page].css
- **Section/Container:** Every content block is `<section class="section [variant]"><div class="container">...</div></section>`
- **Background variants:** `section--white`, `section--surface`, `section--dark`, `section--ocean`
- **On-dark helper:** Add `on-dark` class for white text sections
- **Geo patterns:** Add `pattern-topo`, `pattern-waves`, `pattern-dots`, etc. as classes. Use default (faint) or `-bold` variant.
- **Nav/Footer:** Loaded as HTML partials via `fetch()`. Active link detected by JS matching `window.location.pathname`.
- **Naming:** BEM-ish: `.component`, `.component__element`, `.component--modifier`
- **Design tokens:** All colors, spacing, fonts defined in `tokens.css` as CSS custom properties
- **Contact page:** Uses `mailto:` link, not a form backend. The `.contact-cta` classes handle the centered layout (no inline styles).
- **Footer copyright:** Dynamic year via `document.write(new Date().getFullYear())`

### Key colors (from tokens.css):
- `--color-deep: #2B4759` (deep coastal blue, nav/footer/headings)
- `--color-ocean: #3A5C6F` (ocean harbor blue, primary brand)
- `--color-sage: #7FAE9B` (coastal sage green, secondary)
- `--color-coral: #FF6A5C` (electric coral, accents/hover)
- `--color-oyster: #D9D7D2` (neutral, section separation)
- `--color-white: #F5F3EE` (coastal white, primary background)
- **theme-color:** `#2B4759` (used in meta tag and webmanifest)

---

## Production Infrastructure

### Every HTML page `<head>` must include (in this order):
1. `<meta charset="UTF-8">`, `<meta name="viewport">`
2. `<meta name="theme-color" content="#2B4759">`
3. `<link rel="dns-prefetch" href="https://www.googletagmanager.com">`
4. Google Analytics 4 script block (tag ID: `G-V69H5SY1FS`)
5. `<title>`, `<meta name="description">`, `<meta name="robots">`, GEO meta tags, canonical URL
6. `<meta property="og:locale" content="en_US">` + full OG tags (og:type, og:title, og:description, og:url, og:image with dimensions)
7. Twitter Card tags
8. JSON-LD structured data (appropriate type + BreadcrumbList)
9. Favicon block: `<link rel="icon" href="/favicon.ico">`, PNG favicon, apple-touch-icon, manifest link
10. Google Fonts preconnect + stylesheet
11. Design system CSS chain

### Netlify Configuration

**`_headers`** includes:
- Security: X-Frame-Options (DENY), X-Content-Type-Options (nosniff), Referrer-Policy, Permissions-Policy, X-XSS-Protection, HSTS (preload), X-Robots-Tag
- Content-Security-Policy: whitelists self, Google Analytics, Google Fonts (script-src, style-src, img-src, font-src, connect-src)
- Cache: images (1 year immutable), CSS (30 days), HTML (must-revalidate)

**`_redirects`** includes:
- HTTP to HTTPS enforcement
- www to root domain redirect
- Clean URL aliases (`/about` serves `about.html`, etc.)
- `/* /404.html 404` catch-all at the bottom

### Analytics
- **Google Analytics 4** on all 11 pages (including 404)
- **Privacy policy** updated to disclose GA usage with opt-out link
- **GA tag ID:** `G-V69H5SY1FS`

### Image Guidelines
- Hero images should be under 600KB (currently hero-home.jpg is ~578KB at 1600px wide)
- Mobile hero variants at 768px wide
- OG images must be landscape 1200x630 (use og-home.jpg)
- All images have `width`/`height` attributes and `alt` text
- Use `loading="lazy"` for below-fold images, `loading="eager"` for heroes

---

## SEO / GEO / LLM Optimization

Implemented across the site:
- **JSON-LD** structured data on every page (LocalBusiness, BlogPosting, CollectionPage, ContactPage, AboutPage, OfferCatalog, BreadcrumbList, WebSite)
- **Open Graph** with `og:locale`, dimensions, and landscape images
- **Twitter Card** meta tags
- **GEO meta tags:** `geo.region=US-SC`, `geo.placename=Charleston`
- **robots.txt** explicitly allows LLM crawlers (GPTBot, Claude-Web, Anthropic-AI, PerplexityBot, Google-Extended, Cohere-AI)
- **sitemap.xml** with 10 pages, priorities, and lastmod dates
- **X-Robots-Tag** header: `index, follow`
- **Canonical URLs** on every page pointing to `https://gingerlyfarms.com/...`

---

## Field Notes Section

Styled after Olyticsolutions.com/insights. Text-forward, editorial design. No images on cards.

- **Dark hero banner** with topo pattern overlay
- **Text-only cards** with colored top border (`border-top: 3px solid var(--color-sage)`)
- **Coming soon cards** are greyed out (`fn-card--soon`, opacity 0.45)
- **Article pages** have breadcrumb trail, subtitle, meta line (author / read time / date), and stat blocks
- **Stat blocks:** Dark background, 3-column grid with big numbers and labels

### Current articles:
- **How We Grow** (how-we-grow.html) — Our hydroponic process (Our Process tag)
- **How We Use Water** (why-water-matters.html) — Water usage in our system (How It Works tag)

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
- **No inline styles** in HTML. Move all styling to the appropriate CSS file.
- Keep the Olytics-inspired codebase analysis file (`CODEBASE-ANALYSIS-FOR-GINGERLY-FARMS.md`) as a reference but don't modify it.

---

## New Page Checklist

When adding a new page to the site:

- [ ] Copy the full `<head>` pattern from an existing page (includes all meta tags, GA, favicons, etc.)
- [ ] Set unique `<title>`, `<meta name="description">`, canonical URL
- [ ] Add `<meta name="theme-color" content="#2B4759">`
- [ ] Add `<link rel="dns-prefetch" href="https://www.googletagmanager.com">`
- [ ] Add Google Analytics script block
- [ ] Add `<meta property="og:locale" content="en_US">` and full OG/Twitter tags
- [ ] Add JSON-LD structured data (appropriate type + BreadcrumbList)
- [ ] Add favicon.ico, PNG favicon, apple-touch-icon, manifest links
- [ ] Create page-specific CSS file in `design-system/`
- [ ] Add to `sitemap.xml` with appropriate priority
- [ ] Add to `nav.html` and/or `footer.html` if it belongs in navigation
- [ ] Add clean URL alias in `_redirects` (e.g., `/newpage /newpage.html 200`)

## Update Checklist

When modifying existing pages:

- [ ] Does new copy match the voice/tone guidelines?
- [ ] Are meta descriptions updated to match content changes?
- [ ] Is JSON-LD structured data updated?
- [ ] Is `sitemap.xml` lastmod date updated?
- [ ] No em dashes in visible copy?
- [ ] Email references use contact@gingerlyfarms.com?
- [ ] CSS uses existing design tokens (not hardcoded values)?
- [ ] No inline styles added to HTML?
- [ ] OG images are landscape 1200x630?

---

*Last updated: March 26, 2026*
