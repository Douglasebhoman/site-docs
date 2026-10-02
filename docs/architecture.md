# Architecture

## Page structure convention

Every page on this site follows the same structural rule without exception:

| Concern | Location |
| --- | --- |
| Global styles | `styles.css` — linked from every page |
| Page-specific styles | `<style>` block in `<head>` of each page |
| JavaScript interactions | `<script>` block before `</body>` of each page |
| No per-page CSS files | All page-specific overrides stay inline |
| No external JS libraries | All interactions are vanilla JavaScript |

When editing any page, follow this convention. Do not move styles to
`styles.css` unless they apply to every page on the site.

## Repository structure

```
douglasebhoman.github.io/
├── .github/
│   └── workflows/
│       └── deploy.yml           Builds the site with Eleventy and deploys it to GitHub Pages
├── _includes/
│   └── layouts/
│       └── post.html            Shared layout for every blog post
├── assets/
│   ├── files/                   Downloadable files, such as the CV
│   └── images/                  Images, card images and share images
├── audit/
│   └── index.html
├── blog/
│   ├── index.html               Blog index, generated from the posts collection
│   └── posts/
│       └── <slug>/
│           └── index.html       One folder per post: front matter and body only
├── scripts/
│   ├── drift-check.sh           Fails on outdated or unverifiable claims
│   └── og/                      Share card sources, never published
├── services/
│   └── index.html
├── work/
│   └── index.html
├── .gitignore
├── .nojekyll
├── 404.html
├── CNAME
├── eleventy.config.js
├── index.html
├── package.json
├── package-lock.json
├── README.md
├── robots.txt
├── sitemap.njk
└── styles.css
```

The documentation you are reading lives in the separate [site-docs](https://github.com/Douglasebhoman/site-docs) repository. See [Maintaining These Docs](maintaining-these-docs.md).

## Key files

### index.html

The homepage. Contains all homepage sections inline: hero, gold strip,
impact metrics, about, health check widget, selected work, writing samples,
documentation audit, process steps, social proof, final CTA, and footer.
The most JavaScript-heavy page on the site. See [JavaScript](javascript.md)
for full interaction documentation.

### styles.css

The global stylesheet shared across every page. Contains brand tokens,
layout rules, navigation, footer, and shared component styles. The rule
is simple: if a style applies to more than one page, it belongs here.
If it applies to one page only, it belongs in that page's `<style>` block.

### eleventy.config.js

The Eleventy configuration. It lists the files copied to the build unchanged (`assets/`, `CNAME`, `.nojekyll`, `robots.txt`, `styles.css`, `404.html`, and any `.ico`, `.png` or `.webmanifest` file in the root), excludes `node_modules/`, `_site/`, `README.md` and `scripts/` from the build, and defines two collections:

| Collection | Contents | Order |
| --- | --- | --- |
| `posts` | Every `blog/posts/*/index.html` that has a `part` value and is not marked `draft: true` | Newest first |
| `postsAsc` | The same posts | Oldest first |

It also defines the `pad` filter, which turns `7` into `07`, and the `findByPart` filter, which finds a post by its `part` number. The build output goes to `_site/`.

### package.json

Declares the only dependency, `@11ty/eleventy` 3.1.6, and two scripts:

| Script | Command | Use |
| --- | --- | --- |
| `npm start` | `eleventy --serve` | Local preview with live reload |
| `npm run build` | `eleventy` | One-off build into `_site/` |

`package-lock.json` pins the exact versions that `npm ci` installs.

### _includes/layouts/post.html

The shared layout for every blog post. It renders the head and meta tags, navigation, banner, hero, part navigation, the post body, the "Continue the series" cards, comments, newsletter and footer. Previous and next links come from the `postsAsc` collection, by `part` number.

### .github/workflows/deploy.yml

The workflow **Build and Deploy to GitHub Pages**. Every push to `main` installs dependencies with `npm ci`, builds with Eleventy on Node 22, and deploys `_site/` to GitHub Pages. See [Deployment](deployment.md).

### scripts/

Maintenance scripts. Eleventy ignores this folder, so nothing in it is published.

- `drift-check.sh` fails if any HTML page contains a claim that no longer matches the verifiable record. Run it with `bash scripts/drift-check.sh` before merging.
- `og/` holds the HTML sources for the share images, and a README that explains how to render them.

### work/index.html

The work page at `/work/`. Displays the full portfolio grid. Each card
follows the same structure: banner image, work number, tags, title,
before/after block, outcome line, and a read link. Adding a new card
means duplicating an existing card block and updating the content.
The "Latest writing" strip at the bottom is generated from the three newest posts.

### services/index.html

The services page at `/services/`. Documents the Documentation Audit
service in full: deliverables, pricing, FAQ, and booking CTA. Follows
the standard page structure convention.

### audit/index.html

The audit page at `/audit/`. A standalone booking page linked from the
nav and CTA sections. Contains the Calendly embed and supporting copy.
Follows the standard page structure convention.

### blog/index.html

The blog index at `/blog/`. The featured post, the series navigation strip and the article grid are generated from the posts collection, so publishing a post needs no edit here. The hero, the newsletter embed and the "Coming next" card are written by hand.

### blog/posts/[slug]/index.html

Each blog post lives in its own folder. The folder name is the URL slug.
The file holds front matter and the body HTML only. The shared layout adds everything else at build time. See [Content Guide](content-guide.md#adding-a-blog-post) for the front matter fields.

### CNAME

Declares `douglasebhoman.com` as the custom domain for GitHub Pages.
Must match the DNS CNAME record in Cloudflare. Do not edit this file
unless the domain is changing.

### sitemap.njk

Generates `/sitemap.xml`. It is part generated and part written by hand. The blog post entries come from the posts collection: each location is the post's `canonicalUrl`, and each date is parsed from its `publishDate`. Every other entry is written by hand, with a fixed `<lastmod>` date. When you add, remove or rename a page that is not a post, update its entry here. See [Publishing Checklist](publishing-checklist.md).

### robots.txt

Crawler directives. Currently allows all crawlers. No changes needed
unless specific pages need to be excluded from indexing.

## Stylesheets

| Scope | Location |
| --- | --- |
| Global styles | `styles.css` |
| Page-specific styles | `<style>` block in `<head>` of each page |

## Design tokens

All tokens are CSS custom properties defined at `:root` in `styles.css`.
Reference these tokens in all new CSS. Do not use raw hex values.

### Colour

| Token | Value | Usage |
| --- | --- | --- |
| `--navy` | `#18222C` | Primary dark background |
| `--navy-mid` | `#1E2D3D` | Secondary dark surface |
| `--navy-light` | `#243044` | Tertiary dark surface |
| `--cream` | `#F9F7F4` | Primary light background |
| `--cream-2` | `#F2EFE9` | Secondary light background for alternating sections and inset blocks |
| `--white` | `#FFFFFF` | Defined but not used by any page |
| `--gold` | `#B8962E` | Primary accent — CTAs, labels, borders |
| `--gold-light` | `#D4B060` | Hover and highlight variant |
| `--gold-subtle` | `rgba(184,150,46,0.08)` | Faint gold fill behind tags, icons, pull quotes and step numbers |
| `--gold-border` | `rgba(184,150,46,0.20)` | Faint gold border on tags, buttons, options and callouts |
| `--text-dark` | `#111827` | Primary body text on light backgrounds |
| `--text-mid` | `#4B5563` | Secondary body text on light backgrounds, including blog post body copy |
| `--text-muted` | `#9CA3AF` | De-emphasised text |
| `--text-dim` | `rgba(255,255,255,0.45)` | Subheadings and supporting text on dark backgrounds |
| `--text-ghost` | `rgba(255,255,255,0.25)` | Faintest text on dark backgrounds, used for the hero stat labels |
| `--border-light` | `rgba(0,0,0,0.08)` | Dividers and borders on light surfaces |
| `--border-dark` | `rgba(255,255,255,0.06)` | Dividers and borders on dark surfaces, including the navigation |
| `--green` | `#4ADE80` | Availability indicator |

### Typography

| Token | Value | Usage |
| --- | --- | --- |
| `--serif` | `'Fraunces', Georgia, serif` | Headlines, pull quotes, blog body |
| `--sans` | `'DM Sans', system-ui, sans-serif` | Body text, UI copy |
| `--mono` | `'DM Mono', monospace` | Labels, tags, metadata, code |

### Layout

| Token | Value | Purpose |
| --- | --- | --- |
| `--container` | `960px` | Maximum content width |
| `--pad` | `clamp(24px, 5vw, 48px)` | Responsive horizontal padding |
| `--fast` | `0.15s ease` | Quick transitions — hover states |
| `--base` | `0.25s ease` | Standard transitions — cards, panels |

## Responsive breakpoints

| Breakpoint | Width | What changes |
| --- | --- | --- |
| Desktop | Above `768px` | Full layout — two-column sections, side-by-side footer grid, inline nav links |
| Mobile | `768px` and below | Nav collapses to hamburger menu, footer grid stacks to single column, hero stats switch to 2×2 grid, about section drops to single column |
| Small mobile | `480px` and below | Reduced padding, smaller type scale, single-column contact grid |