# Local Setup

This page covers running the main website on your machine. To work on this documentation site, see [Maintaining These Docs](maintaining-these-docs.md).

## Prerequisites

| Tool | Version | Check with |
| --- | --- | --- |
| Node.js | 22 (matches the deploy workflow) | `node --version` |
| npm | Bundled with Node 22 | `npm --version` |
| Git | Tested with 2.52.0 | `git --version` |
| Web browser | Current release of Chrome, Firefox, Edge or Safari | Browser **About** page |
| GitHub account | Write access to `Douglasebhoman/douglasebhoman.github.io` | Not applicable |

Eleventy 3.1.6 is installed by npm from `package.json`. You do not install it separately.

## Step-by-step guide

1. Clone the repository and move into it:

    ```bash
    git clone https://github.com/Douglasebhoman/douglasebhoman.github.io.git
    cd douglasebhoman.github.io
    ```

2. Install the exact dependency versions from the lockfile:

    ```bash
    npm ci
    ```

3. Start the local server:

    ```bash
    npm start
    ```

    This runs `eleventy --serve`. It builds the site into `_site/`, serves it, and rebuilds when you save a file.

4. Open the address Eleventy prints in the terminal, normally `http://localhost:8080`.

5. Stop the server with `Ctrl+C`.

!!! warning "Do not open the source files directly"
    Blog post files contain only front matter and a body. The shared layout adds the head, navigation and footer at build time. Opening a source file in the browser, or serving the repository with Live Server, shows an unstyled fragment. Always preview through `npm start`.

## Previewing pages locally

| Page | Local URL |
| --- | --- |
| Homepage | `http://localhost:8080/` |
| Work | `http://localhost:8080/work/` |
| Services | `http://localhost:8080/services/` |
| Audit | `http://localhost:8080/audit/` |
| Blog index | `http://localhost:8080/blog/` |
| Blog post | `http://localhost:8080/blog/posts/post-slug/` |
| Sitemap | `http://localhost:8080/sitemap.xml` |
| 404 | `http://localhost:8080/404.html` |

## Build without serving

```bash
npm run build
```

This writes the site to `_site/` exactly as the deploy workflow does. Use it to confirm a change builds cleanly before you push. `_site/` is ignored by Git and must never be edited by hand or committed.

## Check for outdated claims

```bash
bash scripts/drift-check.sh
```

The script fails if a page contains a claim that no longer matches the verifiable record. It must print `drift-check: clean` before you merge.

## Notes

- The MailerLite newsletter form and Giscus comments load from external domains and need an internet connection.
- The documentation health check widget runs entirely in the browser and works offline.
- Posts marked `draft: true` render locally. See [Content Guide](content-guide.md) for what the flag does on the live site.
