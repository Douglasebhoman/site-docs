# Content Guide

This guide covers how to update every page type on the site. Each section
maps to a specific page or component. Find the section for what you are
updating and follow the steps in order.

For stylesheet conventions, see [Architecture](architecture.md).
For JavaScript interactions, see [JavaScript](javascript.md).

---

## Adding a blog post

A post is one file: `blog/posts/<slug>/index.html`. It contains front matter and the body HTML only. The shared layout, `_includes/layouts/post.html`, adds the head, navigation, hero, series navigation, comments, newsletter and footer at build time. Do not paste a page shell into a post.

Publishing a post updates the blog index, the work page's "Latest writing" strip, the neighbouring posts' previous and next links, and the sitemap. You do not edit any of them.

### 1. Create the folder and file

```
blog/
└── posts/
    └── your-post-slug/
        └── index.html
```

Folder naming rules:

- Lowercase letters and hyphens only
- No spaces, no uppercase, no special characters
- The folder name is the URL slug, and must match `canonicalUrl`

### 2. Write the front matter

```yaml
---
layout: layouts/post.html
part: 9
title: "Your Post Title"
description: "Meta description."
ogDescription: "Open Graph description."
twitterDescription: "Twitter description."
ogImage: "https://douglasebhoman.com/assets/images/your-post-slug-cover.png"
canonicalUrl: "https://douglasebhoman.com/blog/posts/your-post-slug/"
seriesTag: "Systems Over Sentences &middot; Part 09 of 10"
postSubtitle: "The subtitle shown in the hero."
publishDate: "September 25, 2026"
readTime: "8 min read"
cardImage: "your-post-slug-cover.png"
cardDate: "September 2026"
cardExcerpt: "The excerpt shown on cards."
pullQuote: "The pull quote shown on the featured card."
---
```

Required fields:

| Field | Meaning |
| --- | --- |
| `layout` | Always `layouts/post.html` |
| `part` | Series number. A post without it is left out of every listing. It sets the order and the previous and next links |
| `title` | Post heading, card title and image alt text |
| `description`, `ogDescription`, `twitterDescription` | Meta, Open Graph and Twitter descriptions |
| `ogImage` | Absolute URL of the share image |
| `canonicalUrl` | Canonical link. Also used as the post's sitemap location |
| `seriesTag` | Hero label, for example `Systems Over Sentences &middot; Part 09 of 10` |
| `postSubtitle` | Hero subtitle. May contain HTML |
| `publishDate` | Displayed date. Must be in the form `September 25, 2026`, because the sitemap parses it |
| `readTime` | Displayed read time |
| `cardImage` | File name in `assets/images/`, used on cards and as the default banner |
| `cardDate`, `cardExcerpt`, `pullQuote` | Card date in the form `September 2026`, card excerpt and pull quote |

Optional fields:

| Field | Meaning |
| --- | --- |
| `draft` | See [Drafts](#drafts) |
| `banner` | Shows the hero banner |
| `bannerImage` | Replaces `cardImage` in the banner |
| `pageTitle`, `ogTitle` | Override the page title and the Open Graph title |
| `jsonLd` | Adds structured data |
| `extraCss` | Loads extra styles. Values: `posts01to04`, `posts06to07` |
| `newsletter*` | Adjust the newsletter block |

Older posts still carry `partNav`, `relatedPrev`, `relatedNext` and `nextDisabledLabel`. Nothing reads these fields. Do not add them to new posts.

### 3. Write the body

Below the front matter, write the post body as HTML. Start at the first paragraph or heading of the article. Do not include `<html>`, `<head>`, navigation or footer.

### 4. Add the images

Place the file named in `cardImage` in `assets/images/`. If `ogImage` points to a different file, add that too. A missing image does not fail the build.

### 5. Preview

```bash
npm start
```

Check the post, `/blog/`, `/work/` and `/sitemap.xml`.

### 6. Publish

Work through [Publishing Checklist: Publish a blog post](publishing-checklist.md#publish-a-blog-post), then commit on a branch and merge:

```bash
git switch -c content/part-NN
git add blog/posts/your-post-slug assets/images
git commit -m "feat: publish Part NN, Your Post Title"
git push origin content/part-NN
```

### Drafts

`draft: true` removes a post from the posts collections. The post then does not appear on the blog index, the work page, the series navigation or the sitemap.

!!! warning "A draft is still published at its own URL"
    The flag hides a post from every listing, but Eleventy still builds the page, and it is deployed. Anyone who has the URL can read it. To keep a post fully private until launch, do not merge it into `main`.

---

## Updating the work page

The work page lives at `work/index.html`.

### Adding a portfolio card

Each card follows this structure:

```html
<a href="/your-portfolio-piece/" class="work-card reveal reveal-d1">
  <div class="work-banner">
    <img class="work-banner-img"
      src="../assets/images/your-card-image.png"
      alt="Alt text" />
    <span class="work-banner-tag">Category</span>
  </div>
  <div class="work-body">
    <div class="work-num">0?</div>
    <div class="work-tags">
      <span class="work-tag">Tag One</span>
      <span class="work-tag">Tag Two</span>
    </div>
    <p class="work-ctitle">Portfolio Piece Title</p>
    <div class="work-ba">
      <div class="work-ba-block before">
        <p class="work-ba-label">The problem</p>
        <p class="work-ba-text">One sentence describing the problem.</p>
      </div>
      <div class="work-ba-block">
        <p class="work-ba-label after">What I built</p>
        <p class="work-ba-text">One sentence describing what you built.</p>
      </div>
    </div>
    <p class="work-outcome"><strong>Result:</strong> One sentence outcome.</p>
    <div class="work-foot">
      <span class="work-link">Read the documentation</span>
      <span class="work-arrow">→</span>
    </div>
  </div>
</a>
```

Rules:
- Increment `work-num` sequentially
- Use `reveal-d1` and `reveal-d2` alternately for staggered animation
- Add the card image to `assets/images/` before pushing
- If the piece has its own URL, follow [Publishing Checklist: Add or remove a portfolio piece](publishing-checklist.md#add-or-remove-a-portfolio-piece)

### Removing a portfolio card

Removing a card requires four steps beyond deleting the block:

1. **Resequence the work numbers** — update every `work-num` value so
   the sequence is unbroken. If you remove card 03, cards 04, 05, and 06
   become 03, 04, and 05.
2. **Rebalance the reveal delay classes** — check that `reveal-d1` and
   `reveal-d2` still alternate correctly across the remaining cards.
3. **Check the homepage** — if the removed piece appeared in the selected
   work grid on `index.html`, replace it with another piece or remove
   the card from that grid too.
4. **Update the sitemap and counts**: follow [Publishing Checklist: Add or remove a portfolio piece](publishing-checklist.md#add-or-remove-a-portfolio-piece).

---

## Updating the services page

The services page lives at `services/index.html`.

The page documents the Documentation Audit service. If the pricing,
deliverables, or FAQ change, edit the relevant section directly in
`services/index.html`. All written content is hardcoded HTML. The one
dynamic component is the Calendly booking embed — it loads from an
external script and renders the booking widget at runtime.

If the Calendly booking link changes, follow [Publishing Checklist: Change the booking link](publishing-checklist.md#change-the-booking-link).

---

## Updating the homepage

The homepage lives at `index.html` in the repository root. All sections
are inline. Page-specific styles are in the `<style>` block in `<head>`.
JavaScript interactions are in the `<script>` block before `</body>`.

This section covers four homepage elements that require content updates:
the selected work grid, the social proof carousel, the typewriter snippets,
and the availability status. For all other homepage JavaScript behaviour,
see [JavaScript](javascript.md).

### Updating the selected work grid

The homepage displays four selected work cards. To swap a card, find the
relevant `.work-card` block in `index.html` and replace its content.
Follow the same card structure as the work page above.

### Updating the social proof carousel

The carousel in the hero side panel has three items. To update an item,
find the `.side-carousel-item` block and edit the text directly. To add
a fourth item:

1. Add a new `.side-carousel-item` div inside `#sideCarouselTrack`
2. Add a new `<button class="side-carousel-dot">` inside `#sideCarouselDots`
3. The carousel JavaScript handles the rest automatically

### Updating the typewriter snippets

The typewriter cycles through three code snippets in the hero panel.
Find the `twSnippets` array in the `<script>` block and edit the strings
directly. Each string supports `\n` for line breaks.

### Updating availability status

The availability indicator appears in two places on the homepage:

- Hero badge: `<div class="hero-badge">`
- Footer: `<div class="f-avail">`

Update both when availability changes.

---

## Updating the footer

Blog post footers come from the shared layout, `_includes/layouts/post.html`. A change there reaches every post at the next build, so posts are not in the list below.

The footer on every other page is hard-coded in that page. It is not a shared component. If the footer content changes (navigation links, contact details, copyright year or tagline), apply the change to each of these files by hand:

- `index.html`
- `work/index.html`
- `services/index.html`
- `audit/index.html`
- `blog/index.html`
- `_includes/layouts/post.html`, for blog posts

`404.html` has no footer.

Use VS Code's global find and replace (`⌘⇧H` on Mac, `Ctrl+Shift+H` on
Windows) to apply footer changes across all files simultaneously.
