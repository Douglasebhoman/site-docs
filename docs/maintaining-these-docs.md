# Maintaining These Docs

This page covers the documentation site you are reading now: how to install it, preview changes locally, and publish them. For the main website, see [Local Setup](local-setup.md) and [Deployment](deployment.md).

## How the docs are built

| Item | Value |
| --- | --- |
| Source repository | [Douglasebhoman/site-docs](https://github.com/Douglasebhoman/site-docs) |
| Generator | MkDocs 1.6.1 with Material for MkDocs 9.7.6 |
| Source files | Markdown in `docs/`, configuration in `mkdocs.yml` |
| Pinned dependencies | `requirements.txt` |
| Build and publish | GitHub Actions workflow `.github/workflows/deploy.yml` |
| Published branch | `gh-pages` (generated, never edited by hand) |
| Live URL | `https://douglasebhoman.com/site-docs/` |

The docs are a GitHub Pages project site. Because the user site (`douglasebhoman.github.io`) has a custom domain, GitHub serves this project at `douglasebhoman.com/site-docs/` automatically. No DNS change is needed for the docs.

## Prerequisites

| Tool | Version | Check with |
| --- | --- | --- |
| Python | 3.12 (matches the workflow) | `python --version` |
| pip | Bundled with Python 3.12 | `pip --version` |
| Git | Tested with 2.52.0 | `git --version` |
| MkDocs | 1.6.1 (installed from `requirements.txt`) | `mkdocs --version` |
| Material for MkDocs | 9.7.6 (installed from `requirements.txt`) | `pip show mkdocs-material` |

## Install

1. Clone the repository and move into it:

    ```bash
    git clone https://github.com/Douglasebhoman/site-docs.git
    cd site-docs
    ```

2. Create and activate a virtual environment, so the pinned versions do not collide with other Python projects:

    === "macOS and Linux"

        ```bash
        python3 -m venv .venv
        source .venv/bin/activate
        ```

    === "Windows (PowerShell)"

        ```powershell
        python -m venv .venv
        .venv\Scripts\Activate.ps1
        ```

3. Install the pinned dependencies:

    ```bash
    pip install -r requirements.txt
    ```

4. Confirm the install:

    ```bash
    mkdocs --version
    ```

    The output starts with `mkdocs, version 1.6.1`.

The repository's `.gitignore` already excludes `.venv/`.

## Preview locally

```bash
mkdocs serve
```

Open `http://127.0.0.1:8000/site-docs/`. MkDocs serves under `/site-docs/` because that is the path in `site_url`. The preview reloads when you save a Markdown file or `mkdocs.yml`.

Stop the server with `Ctrl+C`.

## Check the build before publishing

```bash
mkdocs build --strict
```

`--strict` turns warnings (broken internal links, pages missing from `nav`) into errors. The deploy workflow runs the same command, so a build that fails here fails in CI too. The generated `site/` folder is excluded by `.gitignore`, so it is never committed.

## Add or rename a page

1. Create the Markdown file in `docs/`, using lowercase letters and hyphens: `docs/your-page-name.md`.
2. Add it to `nav` in `mkdocs.yml`. A page not listed in `nav` still builds but does not appear in the navigation.
3. Run `mkdocs build --strict` to catch broken links.
4. If the navigation changed, update the banner screenshot on the work page. See [Publishing Checklist](publishing-checklist.md#change-the-site-documentation).

## Publish

1. Create a branch:

    ```bash
    git checkout -b docs/short-description
    ```

2. Commit using the [Contributing](contributing.md) conventions:

    ```bash
    git add docs/ mkdocs.yml
    git commit -m "docs: short description of the change"
    git push origin docs/short-description
    ```

3. Open a pull request on GitHub and merge it into `main`.
4. The merge triggers **Deploy MkDocs to GitHub Pages**. It installs the pinned versions, runs `mkdocs build --strict`, then pushes the built site to `gh-pages`.
5. Check the run in the repository's **Actions** tab. When it is green, GitHub starts a second run, **pages build and deployment**, which publishes the `gh-pages` branch. When that run is also green, reload the live page.

Do not run `mkdocs gh-deploy` from your own machine. It publishes whatever is in your working copy, with whatever versions you have installed, and skips review.

To redeploy without a new commit, open **Actions**, select **Deploy MkDocs to GitHub Pages**, and choose **Run workflow**.

## When something goes wrong

See [Deployment: Troubleshooting](deployment.md#troubleshooting) and [Deployment: Rolling back](deployment.md#rolling-back).
