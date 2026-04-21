## What triggers a deployment

Github Pages deployment is triggered automatically on every **Push** or **Merge**

## GitHub Actions workflow

The workflow is pages build deployment, **GitHub own internal workflow**

### Steps:

1. You push to main
2. GitHub detects the push automatically
3. GitHub's built-in Pages workflow  (pages build-deployment) runs
4. No build step, the HTML files are served as-is
5. GitHub serves the contents of main directly as the site

## Where the built site end up

The contents of the main branch are served directly as the live site by GitHub Pages

## Custom domain configuration

DNS maps the custom domain to GitHub IP and GitHub settings confirm that mapping, enabling the site accessed by douglasebhoman.com

1. By adding the custom domain to the DNS provider (Cloudflare) 

2. Added a CNAME that points the domain, (douglasebhoman.com) to GitHub Pages URL (douglasebhoman.github.io) 

3. Specified custom domain in GitHub settings.

## Deployments time

typically 1-2 minutes depending on GitHub Actions queue time.

## Verifying deployment

After pushing, navigate to the Actions tab in the GitHub repository to monitor the workflow status. **A green checkmark confirms the deployment was successful**