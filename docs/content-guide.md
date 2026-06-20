# Content Guide

This guide covers how to update every page type on the site. Each section
maps to a specific page or component. Find the section for what you are
updating and follow the steps in order.

For stylesheet conventions, see [Architecture](architecture.md).
For JavaScript interactions, see [JavaScript](javascript.md).

---

## Adding a blog post

### 1. Create the folder and file

Each blog post lives in its own folder inside `blog/posts/`. The folder
name becomes the URL slug.

blog/

└── posts/

└── your-post-slug/

└── index.html

Folder naming rules:
- Lowercase letters and hyphens only
- No spaces, no uppercase, no special characters
- The folder name must match the intended URL exactly

correct:   anatomy-of-great-documentation

incorrect: Anatomy of Great Documentation

incorrect: anatomy_of_great_documentation

### 2. Build the HTML structure

Every post `index.html` must include the following sections in order.

**Navigation**

```html
<nav class="nav" id="nav">
  <a href="/" class="nav-logo">Douglas Ebhoman</a>
  <div class="nav-links" id="navLinks">
    <a href="/work/"     class="nav-text">Work</a>
    <a href="#samples"   class="nav-text">Samples</a>
    <a href="/services/" class="nav-text">Services</a>
    <a href="/audit/"    class="nav-text">Audit</a>
    <a href="#about"     class="nav-text">About</a>
    <a href="/blog/"     class="nav-text nav-text--active">Blog</a>
  </div>
  <button class="nav-hamburger" id="navHamburger" aria-label="Open menu"
    aria-expanded="false">
    <span></span><span></span><span></span>
  </button>
</nav>
```

**Post hero**

```html
<section class="post-hero">
  <div class="post-hero-inner">
    <a href="/blog/" class="post-back">← All posts</a>
    <span class="post-series-tag">Systems Over Sentences · Part ? of 10</span>
    <h1 class="post-title">Post Title</h1>
    <p class="post-subtitle">Subtitle</p>
    <div class="post-meta">
      <span class="post-meta-item">Douglas Ebhoman</span>
      <span class="post-meta-item">Published Month Day, Year</span>
      <span class="post-meta-item">X min read</span>
    </div>
  </div>
</section>
```

**Cover image**

```html
<div class="post-cover">
  <img
    src="../../../assets/images/post-slug-cover.png"
    width="1200"
    height="630"
    loading="eager"
  />
</div>
```

Cover image naming convention: `post-slug-cover.png`
Example: `anatomy-of-great-documentation-cover.png`

Place the cover image in `assets/images/` before pushing.

**Post body**

```html
<div class="post-body-wrap">
  <article class="post-body">
    <!-- Post content here -->
  </article>
</div>
```

**Series navigation**

For posts that are not the last in the series:

```html
<nav class="series-nav">
  <a href="/blog/" class="series-nav-link">← All posts</a>
  <a href="/blog/posts/next-post-slug/"
    class="series-nav-link series-nav-link--next">
    Part ?: Next Post Title →
  </a>
</nav>
```

For the last post in the series, omit the next link:

```html
<nav class="series-nav">
  <a href="/blog/" class="series-nav-link">← All posts</a>
</nav>
```

**Comments**

```html
<section class="comments-section">
  <p class="comments-label">Discussion</p>
  <script src="https://giscus.app/client.js"
    data-repo="Douglasebhoman/douglasebhoman.github.io"
    data-repo-id="R_kgDORhvuTg"
    data-category="Announcements"
    data-category-id="DIC_kwDORhvuTs4C53Ys"
    data-mapping="pathname"
    data-strict="0"
    data-reactions-enabled="1"
    data-emit-metadata="0"
    data-input-position="bottom"
    data-theme="preferred_color_scheme"
    data-lang="en"
    data-loading="lazy"
    crossorigin="anonymous"
    async>
  </script>
</section>
```

**Newsletter**

```html
<section class="post-newsletter">
  <div class="post-newsletter-inner">
    <div>
      <p class="post-newsletter-label">Newsletter</p>
      <p class="post-newsletter-desc">
        One post a week on how documentation actually works.<br>
        No spam. Unsubscribe anytime.
      </p>
    </div>
    <script>
      (function(w,d,e,u,f,l,n){w[f]=w[f]||function(){(w[f].q=w[f].q||[])
      .push(arguments);},l=d.createElement(e),l.async=1,l.src=u,
      n=d.getElementsByTagName(e)[0],n.parentNode.insertBefore(l,n);})
      (window,document,'script',
      'https://assets.mailerlite.com/js/universal.js','ml');
      ml('account', '2241731');
    </script>
    <div class="ml-embedded" data-form="8iCjwu" style="width: 100%;"></div>
  </div>
</section>
```

**Footer**

```html
<footer class="post-footer">
  <div class="post-footer-inner">
    <p class="post-footer-text">
      © 2026 Douglas Ebhoman · Narrative is infrastructure. I treat it that way.
    </p>
    <a href="/blog/" class="post-footer-link">← Back to blog</a>
  </div>
</footer>
```

### 3. Update the blog index

Open `blog/index.html` in VS Code. Add the new post card to the article
grid. Follow the existing card structure — duplicate the most recent card
and update the slug, title, date, and description.

### 4. Update sitemap.xml

Add a new `<url>` entry to `sitemap.xml`:

```xml
<url>
  <loc>https://douglasebhoman.com/blog/posts/your-post-slug/</loc>
  <lastmod>YYYY-MM-DD</lastmod>
</url>
```

### 5. Push to main

```bash
git add -A
git commit -m "content: publish Part 07 — Your Post Title Here"
git push origin main
```

Replace `07` with the actual part number and `Your Post Title Here` with
the exact post title before running the commit command.

The post is live within one to two minutes of pushing.

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
- Update `sitemap.xml` if the portfolio piece has its own URL

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
4. **Update `sitemap.xml`** — remove the entry for the piece if it had
   its own URL.

---

## Updating the services page

The services page lives at `services/index.html`.

The page documents the Documentation Audit service. If the pricing,
deliverables, or FAQ change, edit the relevant section directly in
`services/index.html`. All written content is hardcoded HTML. The one
dynamic component is the Calendly booking embed — it loads from an
external script and renders the booking widget at runtime.

If the Calendly booking link changes, update it in these locations:
- `services/index.html` — booking CTA button
- `index.html` — nav CTA, hero CTA, audit section CTA, final CTA
- `audit/index.html` — Calendly embed URL

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

The footer is hardcoded in every HTML file across the site. It is not a
shared component. If the footer content changes — navigation links,
contact details, copyright year, or tagline — the change must be applied
to every HTML file manually.

Files that contain the footer:
- `index.html`
- `work/index.html`
- `services/index.html`
- `audit/index.html`
- `blog/index.html`
- `blog/posts/[every post]/index.html`
- `404.html`

Use VS Code's global find and replace (`⌘⇧H` on Mac, `Ctrl+Shift+H` on
Windows) to apply footer changes across all files simultaneously.