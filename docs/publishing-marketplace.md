# Publishing this action to GitHub Marketplace

Instructions for maintainers of this repository.

## Workflow files are not allowed (official requirement)

GitHub’s documentation for [Publishing actions in GitHub Marketplace](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace) states:

> Each repository must not contain any workflow files.

So **this repository must not** contain `.github/workflows/`. That blocks using GitHub Actions **in this repo** to publish the Antora manual to Pages.

**Live manual:** The HTML manual is built from the `manual/` directory here and published by a **separate** repository:

- **Source (this repo):** `manual/` — playbook, AsciiDoc pages, nav.
- **Publishing repo:** [antora-supplemental/antora-build-action-docs](https://github.com/antora-supplemental/antora-build-action-docs) — contains only a workflow that checks out this repo, runs Antora on `manual/`, and deploys to GitHub Pages.

**Public URL (project site):** https://antora-supplemental.github.io/antora-build-action-docs/

After you change `manual/` on `main`, open the **docs** repo → **Actions** → **Publish manual** → **Run workflow** (or wait for the scheduled run if configured).

### First-time setup (docs repo)

1. Create **antora-supplemental/antora-build-action-docs** on GitHub and push this repository’s workflow and `README.md` (or use the folder shipped beside the action repo in your workspace).
2. In the docs repo: **Settings → Pages** → **Build and deployment** → Source: **GitHub Actions**.
3. Run **Publish manual** from the **Actions** tab once and confirm https://antora-supplemental.github.io/antora-build-action-docs/ loads.

---

1. **Accept terms.** The organization (or you) must accept the [GitHub Marketplace Developer Agreement](https://github.com/marketplace/developer-terms).

2. **Create a release:**
   - Repo → **Releases** → **Draft a new release**.
   - Choose a tag (e.g. `v1.0.0`), add a title and notes.
   - Under **Release Action**, check **Publish this Action to the GitHub Marketplace**.
   - Pick a **Primary category** (e.g. "Continuous integration").
   - Optionally pick **Another category**.
   - **Publish release**.

3. The action will appear on [GitHub Actions Marketplace](https://github.com/marketplace?type=actions) and users can reference it as `antora-supplemental/antora-build-action@v1`.

To update the listing, create a new release (e.g. `v1.0.1`); the marketplace page will show the latest release.

4. **Listing copy.** Marketplace ingests **README.md** only (Markdown). Keep the long-form manual in `manual/` (Antora site); link the live site from **README.md**.
