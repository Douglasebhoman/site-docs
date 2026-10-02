# Publishing Checklist

Eleventy generates most of the surfaces that used to be updated by hand. This page lists what is left: the manual steps for each kind of change, in one place. The [Content Guide](content-guide.md) explains how to edit each file.

Work on a branch, preview with `npm start`, and run both checks before merging:

```bash
npm run build
bash scripts/drift-check.sh
```

## Publish a blog post

Generated for you: the blog index (featured post, series navigation, article grid), the "Latest writing" strip on the work page, previous and next links on neighbouring posts, and the post's sitemap entry.

Manual steps:

- [ ] Create `blog/posts/your-post-slug/index.html` with the front matter in [Content Guide: Adding a blog post](content-guide.md#adding-a-blog-post).
- [ ] Add the card image named in `cardImage` to `assets/images/`. A missing image does not fail the build. It shows as a broken image on every card.
- [ ] Add the share image named in `ogImage`, if it is a new file.
- [ ] Set `publishDate` in the form `September 25, 2026`. The sitemap parses this exact format.
- [ ] Set `seriesTag`, for example `Systems Over Sentences &middot; Part 09 of 10`.
- [ ] Raise the published essay count in `index.html` by one: the hero stat "Published essays" and the "Published essays on documentation systems" metric card. Both are `data-count` values written by hand.
- [ ] Check `blog/index.html` for any hand-written "Coming next" card that names this post, and remove or update it.
- [ ] Check `index.html` for any carousel item or card that names a specific part.
- [ ] Preview the post, the blog index, the work page and `/sitemap.xml` locally.
- [ ] Commit: `feat: publish Part NN, Post Title`.
- [ ] Merge, then [verify the deployment](deployment.md#verifying-a-deployment).

## Publish a post that was committed as a draft

- [ ] Remove `draft: true` from the post's front matter.
- [ ] Set `publishDate` and `cardDate` to the real publication date.
- [ ] Work through every step in [Publish a blog post](#publish-a-blog-post).

## Add a page that is not a blog post

- [ ] Create the page.
- [ ] Add its URL and date to the hand-written entries in `sitemap.njk`.
- [ ] Add Open Graph tags and a share image. See `scripts/og/README.md`.
- [ ] Add it to the navigation and footer on every top-level page, if it belongs there.

## Remove or rename a page

- [ ] Remove or update its hand-written entry in `sitemap.njk`. The sitemap must not list a URL that returns 404.
- [ ] Search for links to the old URL: `grep -rn "old-path" --include="*.html" --include="*.njk" .`

## Add or remove a portfolio piece

- [ ] Edit the card in `work/index.html`. See [Content Guide: Updating the work page](content-guide.md#updating-the-work-page).
- [ ] Resequence every `work-num` and rebalance `reveal-d1` and `reveal-d2`.
- [ ] Update the piece count wherever it appears: the work page hero headline and stat, the work page meta, Open Graph and Twitter descriptions, the homepage hero stat, the homepage "Facts" metric card, and the "All six portfolio pieces" line in the homepage social proof section.
- [ ] Update the homepage selected work grid, if the piece appears there.
- [ ] Add or remove its entry in `sitemap.njk`, if it has its own URL on `douglasebhoman.com`.

## Change the audit price or packages

Buttons do not show a price. The price appears on the price blocks, in statistics and in page descriptions. Most pages write it as `&euro;300`, and the audit page descriptions write it as `€300`, so search for both.

- [ ] Find every instance: `grep -rnE "(&euro;|€)300" --include="*.html" .`
- [ ] `index.html`: hero stat, the "Facts" metric note, both audit price cards, the social proof figure, meta description and `og:description`.
- [ ] `services/index.html`: hero statistic, hero card, price block, FAQ, meta description.
- [ ] `audit/index.html`: price block, meta and share descriptions.
- [ ] `work/index.html`: the line above the audit button.
- [ ] The platform note beneath each price card, if the Upwork packages changed.
- [ ] Update LinkedIn (Experience entry and Featured description) to match.

## Change availability

- [ ] `index.html` hero badge (`.hero-badge`).
- [ ] The footer availability line (`.f-avail`) in `index.html`, `work/index.html`, `services/index.html`, `audit/index.html` and `blog/index.html`.
- [ ] "Limited availability" notes in both audit sections of `index.html`.

## Change the booking link

- [ ] Find every instance: `grep -rn "calendly.com/douglas-douglasebhoman" --include="*.html" .`
- [ ] Update each one, including the embed on `audit/index.html` and the button in `_includes/layouts/post.html`.

## Add a new claim about experience, clients or results

- [ ] Confirm the claim links to something a reader can check.
- [ ] If an old claim is being retired, add its wording to the pattern list in `scripts/drift-check.sh`.

## Change the site documentation

- [ ] Follow [Maintaining These Docs](maintaining-these-docs.md).
- [ ] If the navigation changed, retake the banner screenshot used on the work page and homepage cards.
