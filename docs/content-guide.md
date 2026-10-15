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

This is Part 9's front matter, copied from `blog/posts/information-architecture-in-documentation/index.html`. Every field in it is read by the build.

```yaml
---
layout: layouts/post.html
title: "Your Documentation Is a Series. Your Reader Skipped Part 1."
description: "A series has an order, but readers rarely follow it. Part 9 of Systems Over Sentences, on information architecture as a decision about relationships."
ogDescription: "A series has an order, but readers rarely follow it. Part 9 of Systems Over Sentences, on information architecture as a decision about relationships."
twitterDescription: "A series has an order. Readers rarely follow it."
ogImage: "https://douglasebhoman.com/assets/images/information-architecture-in-documentation.png"
canonicalUrl: "https://douglasebhoman.com/blog/posts/information-architecture-in-documentation/"
publishDate: "September 25, 2026"
readTime: "7 min read"
pageTitle: "Information Architecture in Documentation: Your Reader Skipped Part 1"
keywords: ["information architecture", "technical writing", "documentation structure", "learning paths", "documentation design", "structured writing"]
part: 9
cardDate: "September 2026"
cardImage: "information-architecture-in-documentation.png"
banner: true
cardExcerpt: "This series was replanned mid-flight, because a page already published would not allow the original order. Architecture is a decision about relationships."
pullQuote: "A page should be able to stand on its own without losing its place in the larger story."
---
```

#### Required fields

Every post needs all of these. Without one of the first five, the build fails or the page loses its layout. Without one of the others, the build still succeeds, but part of the page or of the blog listings is empty or broken.

| Field | Read by | Without it |
| --- | --- | --- |
| `layout` | Eleventy. Always `layouts/post.html` | The post is published as its bare body, with no head, navigation or styles |
| `title` | The hero, the Twitter title, the structured data, and the cards on the blog index and the work page | The build fails |
| `description` | The meta description and the structured data. Also the Twitter description, unless `twitterDescription` is set | The build fails |
| `canonicalUrl` | The canonical link, `og:url`, the structured data and the sitemap | The build fails |
| `publishDate` | The hero, the structured data and the sitemap. Must be in the form `September 25, 2026` | The build fails. A date in any other form also fails the build |
| `part` | The series number. It sets the order on the blog index, the series tag, the title suffix and the previous and next links | The post is left out of the blog index, the work page and the sitemap, and has no series tag |
| `ogDescription` | `og:description` | The Open Graph description is empty |
| `ogImage` | `og:image` and `twitter:image`. An absolute URL | Both share image tags are empty |
| `readTime` | The hero and the featured post on the blog index | The read time is blank |
| `cardImage` | A file name in `assets/images/`. The image on the blog index and work page cards, and the banner | The card images are broken |
| `cardDate` | The card date on the blog index, in the form `September 2026` | The card date is blank |
| `cardExcerpt` | The card excerpt on the blog index | The excerpt is blank |
| `pullQuote` | The featured post on the blog index, and the "Continue the series" cards on the neighbouring posts | The quotation marks show with nothing between them |

Structured data cannot contain HTML entities such as `&rsquo;`, because a browser does not decode them inside a script. A `title`, `description`, keyword or citation that contains one fails the build. Type the character itself.

#### Fields with a default

`blog/posts/posts.json` sets these for every post in `blog/posts/`. A post may override either one in its own front matter.

| Field | Default in `posts.json` | Read by |
| --- | --- | --- |
| `postSubtitle` | The author line | The hero subtitle. It may contain HTML |
| `series` | The series `name`, its `total` number of parts, and the blog `url` | The series tag, for example "Systems Over Sentences · Part 09 of 10", the title suffix, the part navigation label and the structured data. A post that overrides only `series.name` keeps the default `total` and `url` |

#### Optional fields

| Field | Effect |
| --- | --- |
| `pageTitle` | The title for search results. For the browser title and `og:title`, the build adds a vertical bar, the series name and the part number after it. Without it, the browser title is the post's `title` followed by "· Douglas Ebhoman", with no series name or part number |
| `ogTitle` | Replaces the assembled page title in `og:title` |
| `twitterDescription` | Replaces `description` in `twitter:description` |
| `banner` | `true` shows `cardImage` as a banner above the hero, and hides the visible post title, which stays available to screen readers |
| `bannerImage` | Shows this file in the banner instead of `cardImage` |
| `keywords` | A list of strings, added to the structured data |
| `citation` | A string, or a list of strings, added to the structured data |
| `draft` | See [Drafts](#drafts) |
| `newsletterShowLabel` | `true` shows the "Stay current" label above the newsletter block |
| `newsletterTitleTag` | The HTML tag for the newsletter heading. Without it, the heading is a `p` |
| `newsletterBtnClass` | The class of the newsletter block's booking button. Without it, the class is `btn-ghost-light` |
| `newsletterNoTarget` | `true` opens the booking link in the same tab |

### 3. Write the body

Below the front matter, write the post body as HTML. Start at the first paragraph or heading of the article. Do not include `<html>`, `<head>`, navigation or footer.

### 4. Add the images

All images live in `assets/images/`, which the blog shares with the rest of the site.

Name the banner with the post's slug exactly, with no suffix. Give it the extension that matches the file's real format: `.png` for a PNG, and `.jpg` or `.jpeg` for a JPEG. For example, Part 9's slug is `information-architecture-in-documentation`, and its banner is a PNG, so the file is `information-architecture-in-documentation.png`. Part 7's banner is a JPEG, so the file is `the-discipline-of-research.jpg`.

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

Draft posts are excluded from production builds entirely. They render only under `npm start`. Remove `draft: true` to publish. Eleventy does not clear `_site/` between builds, so a page that was drafted, deleted or renamed after being published can survive in your local `_site/` and look live when it is not.

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

1. **Resequence the work numbers**: update every `work-num` value so
   the sequence is unbroken. If you remove card 03, cards 04, 05, and 06
   become 03, 04, and 05.
2. **Rebalance the reveal delay classes**: check that `reveal-d1` and
   `reveal-d2` still alternate correctly across the remaining cards.
3. **Check the homepage**: if the removed piece appeared in the selected
   work grid on `index.html`, replace it with another piece or remove
   the card from that grid too.
4. **Update the sitemap and counts**: follow [Publishing Checklist: Add or remove a portfolio piece](publishing-checklist.md#add-or-remove-a-portfolio-piece).

---

## Updating the services page

The services page lives at `services/index.html`.

The page documents the Documentation Audit service. If the pricing,
deliverables, or FAQ change, edit the relevant section directly in
`services/index.html`. All written content is hardcoded HTML. The one
dynamic component is the Calendly booking embed. It loads from an
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
