# Overview

## What this site is

douglasebhoman.com is the professional web presence and freelance practice
of Douglas Ebhoman, a documentation systems specialist based in Prague.
It is a static site built in pure HTML, CSS, and JavaScript. There is no
framework, no build step, and no CMS. The repository contents are the
deployment artefact.

## Project details

| Property | Value |
| --- | --- |
| GitHub repo | https://github.com/Douglasebhoman/douglasebhoman.github.io |
| Live site | https://douglasebhoman.com |
| Tech stack | HTML, CSS, Vanilla JavaScript |
| Build tools | None |
| Deployment | Push to `main` triggers GitHub Pages automatically |

## Site structure

| URL | Page | Purpose |
| --- | --- | --- |
| `/` | Homepage | Hero, health check widget, selected work, writing samples, documentation audit service, social proof, contact, newsletter |
| `/work/` | Work | Full grid of documentation portfolio pieces |
| `/services/` | Services | Documentation Audit service — pricing, deliverables, FAQ |
| `/audit/` | Audit | Standalone audit booking page |
| `/blog/` | Blog index | Systems Over Sentences series — article grid and newsletter |
| `/blog/posts/from-writing-to-documentation-systems/` | Post 01 | From Writing to Documentation Systems |
| `/blog/posts/your-documentation-is-a-bakery/` | Post 02 | Your Documentation is a Bakery. Here's How to Build a Supermarket. |
| `/blog/posts/how-product-teams-actually-handle-documentation/` | Post 03 | How Product Teams Actually Handle Documentation (And Why It Usually Fails) |
| `/blog/posts/writing-for-developers-vs-non-technical-users/` | Post 04 | Writing for Developers vs Non-Technical Users: Why the Difference Matters |
| `/blog/posts/anatomy-of-great-documentation/` | Post 05 | The Anatomy of Great Documentation |
| `/blog/posts/introduction-to-structured-writing/` | Post 06 | Introduction to Structured Writing |
| `/404.html` | 404 | Custom error page with navigation back to the homepage |

## Dependencies

### Fonts

| Property | Value |
| --- | --- |
| Provider | Google Fonts |
| Families | Fraunces, DM Sans, DM Mono |
| Loading method | CDN link in `<head>` on every page |

### Newsletter

| Property | Value |
| --- | --- |
| Provider | MailerLite |
| Account ID | `2241731` |
| Form ID | `8iCjwu` |
| Placement | Homepage contact section, blog index, all blog post pages |
| Welcome sequence | Two-email automation active |

### Comments

| Property | Value |
| --- | --- |
| Provider | Giscus |
| Backend | GitHub Discussions on `douglasebhoman.github.io` |
| Repo ID | `R_kgDORhvuTg` |
| Category ID | `DIC_kwDORhvuTs4C53Ys` |
| Mapping | `pathname` — each post gets its own discussion thread |
| Placement | All blog post pages |

### Booking

| Property | Value |
| --- | --- |
| Provider | Calendly |
| Link | https://calendly.com/douglas-douglasebhoman/30min |
| Placement | Homepage nav, homepage CTA section, services page, audit page |

### Documentation health check widget

| Property | Value |
| --- | --- |
| Type | Rule-based scoring engine |
| Questions | Six |
| Dimensions scored | Accuracy, ownership, findability |
| Output | Score percentage, category label, three dimension health bars, per-answer findings, weakest dimension summary |
| States | Three — questions, results, reset. Reset clears all answers and returns to question one. |
| Placement | Homepage |

## Deployment

Every push to `main` triggers the GitHub Pages `pages-build-deployment`
workflow automatically. There is no build step. The repository is served
as-is. Changes are live within one to two minutes of pushing.

| Property | Value |
| --- | --- |
| Custom domain | `douglasebhoman.com` |
| DNS | Cloudflare — DNS-only mode, proxy disabled |
| HTTPS | Issued automatically by GitHub via Let's Encrypt |

**Cloudflare proxy must remain disabled.** Enabling it breaks GitHub's
certificate issuance.