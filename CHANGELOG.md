# Changelog

## [Unreleased]

### Added

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
