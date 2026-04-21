## Files needed for a new post

To create a blog post, index.html must be created under each posts. same HTML structure as every other posts, defferent content.

## Folder structure

Every post folder carries index.html as a file. each of these posts are governed by the blog folder.

```
├── blog/
│   ├── index.html
│   └── posts/
│       └── post-folder-name/
│           └── index.html
```

## What folder and file need to be named

folder names should use lowercase letters, hyphens instead of spaces.and match the URL slug.
Example: your-documentation-is-a-bakery.

## What HTML file contain at minimum

each index.html files follows a specific structural framework.

1. Nav bar

```html
  <header class="nav-header" id="nav-header">
    <nav class="nav-container">
      <a href="/" class="nav-logo">
        <span class="nav-logo-name">Douglas Ebhoman</span>
        <span class="nav-logo-rule"></span>
      </a>
      <ul class="nav-links" id="nav-links">
        <li><a href="/#work"    class="nav-link">Work</a></li>
        <li><a href="/#about"   class="nav-link">About</a></li>
        <li><a href="/#skills"  class="nav-link">Skills</a></li>
        <li><a href="/blog"     class="nav-link nav-link--active">Blog</a></li>
        <li><a href="/#contact" class="nav-link">Contact</a></li>
      </ul>
      <button class="nav-hamburger" id="nav-hamburger" aria-label="Toggle navigation" aria-expanded="false">
        <span class="hamburger-line"></span>
        <span class="hamburger-line"></span>
        <span class="hamburger-line"></span>
      </button>
    </nav>
  </header>

```

2. Post Hero

```html
<main>
    <section class="post-hero">
      <div class="post-hero-inner">
        <a href="/blog" class="post-back">← All posts</a>
        <span class="post-series-tag">Systems Over Sentences · Part ? of 10</span>
        <h1 class="post-title">Blog Title</h1>
        <p class="post-subtitle">Subtitle</p>
        <div class="post-meta">
          <span class="post-meta-item">Douglas Ebhoman</span>
          <span class="post-meta-item">Published date Year</span>
          <span class="post-meta-item">reading Duration</span>
        </div>
      </div>
    </section>
```
3. Cover Image

```html
<div class="post-cover">
      <img
        src="../../../assets/images/Image Name — Systems Over Sentences Part ?"
        width="1200"
        height="630"
        loading="eager"
      />
    </div>

```

4. Post Body

```html
<div class="post-body-wrap">
      <article class="post-body">

```

5.  Series Nav

```html
    <nav class="series-nav">
      <a href="/blog" class="series-nav-link">← All posts</a>
      <a href="/blog/posts/Link to Next Post" class="series-nav-link series-nav-link--next">Part ?: Next Post Title→</a>
    </nav>

```

6. Comment Section

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
7. Newsletter

```html
 <!-- NEWSLETTER -->
    <section class="post-newsletter">
      <div class="post-newsletter-inner">
        <div>
          <p class="post-newsletter-label">Newsletter</p>
          <p class="post-newsletter-desc">
            One post a week on how documentation actually works.<br>No spam. Unsubscribe anytime.
          </p>
        </div>
        <!-- MailerLite Universal -->
        <script>
          (function(w,d,e,u,f,l,n){w[f]=w[f]||function(){(w[f].q=w[f].q||[])
          .push(arguments);},l=d.createElement(e),l.async=1,l.src=u,
          n=d.getElementsByTagName(e)[0],n.parentNode.insertBefore(l,n);})
          (window,document,'script','https://assets.mailerlite.com/js/universal.js','ml');
          ml('account', '2241731');
        </script>
        <div class="ml-embedded" data-form="8iCjwu" style="width: 100%;"></div>
      </div>
    </section>

  </main>

```

8. Footer

```html
  <footer class="post-footer">
    <div class="post-footer-inner">
      <p class="post-footer-text">© 2026 Douglas Ebhoman · Built with intention.</p>
      <a href="/blog" class="post-footer-link">← Back to blog</a>
    </div>
  </footer>
```

## How blog index get updated

Manually via VS Code, push to main, and updates displayed on the live site.

> **Note:** After creating the post folder and file, add post to blog/index.html manually