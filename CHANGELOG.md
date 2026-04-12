# Changelog

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
