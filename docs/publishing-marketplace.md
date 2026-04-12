# Publishing this action to GitHub Marketplace

Instructions for maintainers of this repository.

## Workflows in the action repository (what is and is not restricted)

Older GitHub documentation sometimes quoted a line suggesting that **no** workflow files may exist in a Marketplace action repository. **That is not a useful summary of current practice (2026).** There is **no blanket prohibition** on having `.github/workflows/` in an action repo.

What is true:

* **CI and quality workflows are normal.** Repositories often ship workflows that run tests, linting, or self-checks on pull requests and `main`. That demonstrates health and is aligned with Marketplace expectations.
* **`action.yml` defines the action; `.github/workflows/` does not ship to consumers.** Workflows under your repo run only in your repository. Users still add their own workflow files and reference your action with `uses:`.
* **User-facing “templates”** belong in **README** (copy-paste YAML), a **template repository**, or separate examples—not as something that magically appears in a consumer’s repo because you committed a file.

Do **not** confuse “workflows for the action’s own CI” with “bundling a workflow that targets someone else’s repository.” The latter is not how users consume actions.

Official reference: [Publishing actions in GitHub Marketplace](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace) (read the current page; policies evolve).

---

## Manual site (GitHub Pages, in this repository)

The Antora **manual** lives under `manual/`. It is built and deployed by **`.github/workflows/publish-manual.yml`** (`upload-pages-artifact` + `deploy-pages`).

**Public URL (project site):** https://antora-supplemental.github.io/antora-build-action/

Triggers: pushes to `main` that touch `manual/**` or the workflow file, **workflow_dispatch**, and a daily **schedule**.

### First-time setup (Pages)

1. Repo **Settings → Pages** → **Build and deployment** → Source: **GitHub Actions** (not “Deploy from a branch”).
2. Run **Actions → Publish manual → Run workflow** once, or push a change under `manual/`.
3. Confirm the site loads at the URL above.

---

## Marketplace publishing checklist

1. **Accept terms.** The organization (or you) must accept the [GitHub Marketplace Developer Agreement](https://github.com/marketplace/developer-terms).

2. **Repository contents (typical expectations):**
   * **`action.yml` or `action.yaml`** at the repo root (or a documented subdirectory if publishing from there).
   * **`README.md`** with clear usage (Marketplace ingests **Markdown from this file** for the listing).
   * **License:** include a valid **`LICENSE`** file that matches how you distribute the action (add one at the repo root if missing).

3. **Create a release:**
   - Repo → **Releases** → **Draft a new release**.
   - Choose a tag (e.g. `v1.0.0`), add a title and notes.
   - Under **Release Action**, check **Publish this Action to the GitHub Marketplace**.
   - Pick a **Primary category** (e.g. "Continuous integration").
   - Optionally pick **Another category**.
   - **Publish release**.

4. The action will appear on [GitHub Actions Marketplace](https://github.com/marketplace?type=actions); users reference it as `antora-supplemental/antora-build-action@v1`. New releases (e.g. `v1.0.1`) update the listing.

5. **Listing copy.** Keep **README.md** concise; deep content lives in `manual/` and the **live manual** URL—link it prominently from **README.md**.
