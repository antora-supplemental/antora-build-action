# Publishing this action to GitHub Marketplace

Instructions for maintainers of this repository.

1. **No workflow files.** This repo must not contain any files under `.github/workflows/`. Marketplace rejects action repos that have workflow files.

2. **Accept terms.** The organization (or you) must accept the [GitHub Marketplace Developer Agreement](https://github.com/marketplace/developer-terms).

3. **Create a release:**
   - Repo → **Releases** → **Draft a new release**.
   - Choose a tag (e.g. `v1.0.0`), add a title and notes.
   - Under **Release Action**, check **Publish this Action to the GitHub Marketplace**.
   - Pick a **Primary category** (e.g. "Continuous integration").
   - Optionally pick **Another category**.
   - **Publish release**.

4. The action will appear on [GitHub Actions Marketplace](https://github.com/marketplace?type=actions) and users can reference it as `antora-supplemental/antora-build-action@v1`.

To update the listing, create a new release (e.g. `v1.0.1`); the marketplace page will show the latest release.

5. **Listing copy.** Marketplace ingests **README.md** only (Markdown). Keep **README.adoc** as the full manual; do not duplicate long examples in **README.md**.
