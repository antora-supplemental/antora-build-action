# Antora Build

Composite GitHub Action that builds an [Antora](https://antora.org) documentation site. Use it in your workflow after `checkout`; pair with `actions/upload-pages-artifact` and `actions/deploy-pages` for GitHub Pages.

## Usage

```yaml
- uses: actions/checkout@v4

- uses: antora-supplemental/antora-build-action@v1
  id: antora
  with:
    playbook: antora-playbook.yml   # optional, default above
    # antora-read-token: ${{ secrets.ANTORA_READ_TOKEN }}  # only if playbook has private content sources

- uses: actions/upload-pages-artifact@v3
  with:
    path: ${{ steps.antora.outputs.site-path }}
```

Then add a deploy job that uses `actions/deploy-pages@4`. For private repos in `content.sources`, pass a PAT as `antora-read-token`. See [antora-deployment.adoc](https://github.com/dev-centr/devcentr/blob/main/docs/modules/publishing/pages/antora-deployment.adoc) (Private repos: GITHUB_TOKEN vs PAT).

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `playbook` | `antora-playbook.yml` | Path to the Antora playbook. |
| `node-version` | `20` | Node.js version. |
| `pnpm-version` | `9` | pnpm version. |
| `antora-read-token` | (none) | Optional PAT so Antora can clone other private repos. Omit if all sources are public or same repo. |

## Outputs

| Output | Description |
|--------|-------------|
| `site-path` | Path to the built site (`build/site`). Use as `path` for `upload-pages-artifact`. |

## Publishing this action to GitHub Marketplace

1. **No workflow files.** This repo must not contain any files under `.github/workflows/`. Marketplace rejects action repos that have workflow files.
2. **Accept terms.** Org (or you) must accept the [GitHub Marketplace Developer Agreement](https://github.com/marketplace/developer-terms).
3. **Create a release:**
   - Repo → **Releases** → **Draft a new release**.
   - Choose a tag (e.g. `v1.0.0`), add a title and notes.
   - Under **Release Action**, check **Publish this Action to the GitHub Marketplace**.
   - Pick a **Primary category** (e.g. "Continuous integration").
   - Optionally pick **Another category**.
   - **Publish release**.
4. The action will appear on [GitHub Actions Marketplace](https://github.com/marketplace?type=actions) and users can reference it as `antora-supplemental/antora-build-action@v1`.

To update the listing, create a new release (e.g. `v1.0.1`); the marketplace page will show the latest release.
