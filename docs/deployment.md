# Deployment

## What triggers a deployment

GitHub Pages deployment triggers automatically on every push or merge
to `main`.

## GitHub Actions workflow

The workflow is `pages-build-deployment`, GitHub's built-in internal
workflow. No custom workflow file is required.

### Steps

1. Push to `main`
2. GitHub detects the push automatically
3. GitHub's built-in Pages workflow (`pages-build-deployment`) runs
4. No build step — the HTML files are served as-is
5. GitHub serves the contents of `main` directly as the live site

## What gets deployed

Every file in the `main` branch is served as a static file. This includes:

- `index.html` at the root, served at `douglasebhoman.com`
- `work/index.html`, served at `douglasebhoman.com/work/`
- `services/index.html`, served at `douglasebhoman.com/services/`
- `audit/index.html`, served at `douglasebhoman.com/audit/`
- `blog/index.html`, served at `douglasebhoman.com/blog/`
- All blog post folders under `blog/posts/`, each served at their
  respective URL
- All assets under `assets/`

## Custom domain configuration

DNS maps the custom domain to GitHub Pages. GitHub settings confirm
that mapping, enabling the site to be accessed at `douglasebhoman.com`.

1. A `CNAME` file in the repository root specifies the custom domain
2. A CNAME record in Cloudflare points `douglasebhoman.com` to
   `douglasebhoman.github.io`
3. The custom domain is confirmed in the repository GitHub Pages settings
4. HTTPS is handled automatically by GitHub via Let's Encrypt
5. Cloudflare DNS records are set to DNS-only with no proxy — required
   for GitHub's certificate issuance to work correctly

**Cloudflare proxy must remain disabled.** Enabling it breaks GitHub's
certificate issuance.

## Deployment time

Typically one to two minutes depending on GitHub Actions queue time.

## Verifying deployment

After pushing, navigate to the Actions tab in the GitHub repository to
monitor the workflow status. A green checkmark confirms the deployment
was successful.

If the deployment fails, click the failed workflow run to read the
error log.