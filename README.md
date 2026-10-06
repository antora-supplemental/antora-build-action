# Antora Site Builder

**Composite GitHub Action** — run [Antora](https://antora.org) in CI and produce a static documentation site (HTML) you can publish anywhere. Typical use is **GitHub Actions** plus [**GitHub Pages**](https://pages.github.com/) (`actions/upload-pages-artifact` and `actions/deploy-pages`). This action **builds only**; it does not deploy by itself.

## Documentation (full manual)

**https://antora-supplemental.github.io/antora-build-action/**

The manual covers prerequisites, every input/output, authentication for private `content.sources`, multi-repo examples, official vs peaceiris Pages patterns, security, and troubleshooting. Source lives under `docs/` in this repository (AsciiDoc playbook + `content/`).

> GitHub Marketplace ingests **this `README.md` only** (Markdown). Keep this file short; put depth in the manual.

## What you get

- **Antora runs** with your playbook (`antora-playbook.yml` or another path), respecting `working_directory` for monorepos.
- **Private Git content** — optional credentials for `content.sources` (GitHub, GitLab, Bitbucket patterns via `git_credentials` or `github_token`).
- **Flexible Antora install** — `antora_mode`: use a project-local `antora` dependency, or **`pnpm dlx` / `npx`** when Antora is not in `package.json` (see the manual).
- **GitHub Pages–friendly output** — optional **`create_nojekyll`** (default **on**) adds `.nojekyll` at the site output root so paths like `_css` / `_js` are served reliably.
- **Outputs** `site-path` / `site_dir` for the next step (for example `upload-pages-artifact`).

## Minimal usage

```yaml
- uses: actions/checkout@v7
- uses: antora-supplemental/antora-build-action@v3
  id: antora
  with:
    playbook: antora-playbook.yml
    output_dir: build/site
- uses: actions/upload-pages-artifact@v5
  with:
    path: ${{ steps.antora.outputs.site-path }}
```

Then use a **deploy** job with `actions/deploy-pages@v5`. Permissions, a two-job example, and alternatives are in the **manual** (link above).

## v2 migration (from v1)

Input names are **positive** defaults (opt out with `false`):

| v1 (removed) | v2 |
|----|----|
| `skip_install: true` | `install_dependencies: false` |
| `skip_pnpm_setup: true` | `setup_pnpm: false` |
| `skip_node_setup: true` | `setup_node: false` |

Use `antora-supplemental/antora-build-action@v3` in workflows. v3 has the same inputs as v2; it only moves the bundled `pnpm/action-setup` and `actions/setup-node` steps to their Node 24 majors (v6 / v7), which removes the "Node.js 20 is deprecated" warning. **`v2` and `v1` remain available** (v1 for existing YAML that still references `skip_*`).
