# Changelog

## [Unreleased]

## v3.0.0 - 2026-10-06

### Changed

- Bundled steps moved to Node 24 majors: `pnpm/action-setup@v6` (was v4) and `actions/setup-node@v7` (was v4). GitHub deprecated Node 20 on the runners (https://github.blog/changelog/2025-09-19-deprecation-of-node-20-on-github-actions-runners/); v2 runs still work but log a deprecation warning.
- Inputs and outputs are unchanged from v2. `actions/setup-node` v5+ can also auto-cache npm when `package.json` declares npm in `packageManager`; this action already passes `cache` explicitly.
- Docs examples, README and this repo's own workflow use current action majors; `.github/dependabot.yml` keeps them current (monthly, grouped).
- `v2` stays at v2.0.0 for existing workflows; new workflows should use `@v3`.

### Added (since v2.0.0)

- Antora `site.robots` emits `/robots.txt` with an absolute Sitemap URL for the production host.

### Changed

- Docs site lockfile refresh so Antora resolves `@asciidoctor/core` 2.2.9; its Opal runtime (0.3.4) uses `fast-glob` instead of the deprecated `glob@7` and `inflight`.

## v2.0.0 — 2026-04-12

### Breaking change: positive toolchain inputs

Replaced **`skip_install`**, **`skip_pnpm_setup`**, and **`skip_node_setup`** with opt-out defaults:

| Input | Default | Meaning |
|-------|---------|--------|
| `install_dependencies` | `true` | Run `pnpm install --frozen-lockfile` or `npm ci` |
| `setup_pnpm` | `true` | Run `pnpm/action-setup` when the repo uses pnpm |
| `setup_node` | `true` | Run `actions/setup-node` with dependency cache |

To mirror old `skip_*: true` behavior, set the corresponding input to `false`.

**`v1` remains** at the previous major release for workflows that still reference `skip_*`. New workflows should use **`antora-supplemental/antora-build-action@v2`**.
