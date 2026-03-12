# Antora Build

**For use in the GitHub Actions workflow editor.** Go to the repository where you want to deploy Antora, open **Actions**, click **Set up a workflow yourself** →, then search for the action's name to add it to your workflow.

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

Maintainers: see [docs/publishing-marketplace.md](docs/publishing-marketplace.md) for how to publish or update the action on GitHub Marketplace.
