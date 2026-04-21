# Contributing

## Naming conventions

All file and folder names must use lowercase letters and hyphens instead of spaces.

```
good: your-documentation-is-a-bakery
bad:  Your Documentation Is A Bakery
```

## Commit message conventions

All commit messages must follow the Conventional Commits format: `type: short description`

| Type | When to use | Example |
|------|-------------|---------|
| `feat:` | Adding something new that didn't exist before | `feat: add Part 4 blog post` |
| `fix:` | Correcting something broken or wrong | `fix: correct broken nav link on mobile` |
| `docs:` | Updating documentation only — site-docs, README, Markdown files | `docs: update architecture section` |
| `style:` | Visual or CSS changes that don't affect functionality | `style: adjust newsletter padding on mobile` |
| `chore:` | Maintenance tasks — reorganising files, renaming folders | `chore: rename assets folder structure` |

## Submitting changes

Never push directly to `main`. This is a live site — broken code pushed to `main` deploys immediately.

Always:
1. Create a new branch for your change
2. Make your changes on that branch
3. Submit a pull request for review
4. Merge to `main` only after review

## Code style

**Indentation:** 2 spaces throughout all HTML and CSS files.

**Class naming:** Use kebab-case — all lowercase, words separated by hyphens.

```
good: nav-header, post-hero-inner, blog-footer-text
bad:  navHeader, PostHeroInner, blogFooterText
```

**CSS location:**
- Global styles that apply across all pages → `styles.css`
- Page-specific styles that apply to one page only → `<style>` tag inside that page's `<head>`

## Reporting bugs and suggestions

If you find a bug or want to suggest an improvement, raise a GitHub Issue on the repository:

[github.com/Douglasebhoman/douglasebhoman.github.io/issues](https://github.com/Douglasebhoman/douglasebhoman.github.io/issues)

Describe the problem or suggestion clearly — include the page affected, what you expected to happen, and what actually happened.