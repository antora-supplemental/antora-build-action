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
- uses: actions/checkout@v4
- uses: antora-supplemental/antora-build-action@v1
  id: antora
  with:
    playbook: antora-playbook.yml
    output_dir: build/site
- uses: actions/upload-pages-artifact@v3
  with:
    path: ${{ steps.antora.outputs.site-path }}
```

Then use a **deploy** job with `actions/deploy-pages@v4`. Permissions, a two-job example, and alternatives are in the **manual** (link above).
