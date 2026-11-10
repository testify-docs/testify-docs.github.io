# Provenance {#provenance}


Every fact needed to reproduce this site byte-for-byte, recorded at generation time.


## Source {#source}


| Field | Value |
| --- | --- |
| Repository | https://github.com/stretchr/testify |
| Commit | `87a7b9d57689f6579db2da795ab8deeab29cb724` |
| Commit date | 2026-09-24 |
| License | MIT (`LICENSE` in the tree, Copyright (c) 2012-2020 Mat Ryer, Tyler Bunnell and contributors) |
| Module | `github.com/stretchr/testify` |

The commit is pinned rather than tracking `master`: the tree was fetched at that exact SHA, so the text on this site cannot change under the reader's feet.


## Generator {#generator}


| Tool | Version |
| --- | --- |
| Sourcey | `3.9.5` (npm package `sourcey`) |
| Adapter | `godoc` (snapshot mode) |
| Node.js | `v24.22.1` |
| Go toolchain | `go1.27.3` (used only to produce the snapshot) |


## Exact commands {#exact-commands}


Sourcey was obtained from the public npm registry:

```bash
npm install sourcey@3.9.5
npm install -g @runxhq/cli   # runx-cli 0.11.1, governs the build run
```

The godoc snapshot was taken from the pinned module tree:

```bash
sourcey godoc --module ./target --packages ./... --out godoc.json
# Sourcey: wrote godoc snapshot for github.com/stretchr/testify
#   Packages:    10
```

The published snapshot (`godoc.json`) was then filtered to the six public packages before building. Removed, with reasons:

- `github.com/stretchr/testify/internal/difflib`, `github.com/stretchr/testify/internal/spew` — vendored forks under `internal/`; not importable public API.
- `github.com/stretchr/testify/assert/internal/unsafetests` — internal test helper.
- `github.com/stretchr/testify/assert/yaml` — vendored YAML fork used by `assert`; not public API surface.

The site was built from the filtered snapshot:

```bash
sourcey build -c sourcey.config.ts -o dist
```


## Governed run {#governed-run}


The snapshot and build were executed as a governed [runx](https://runx.ai) skill run so the work carries a sealed, recomputable receipt. The delivery packet for this publication records the run's `receipt_ref`, the exact `runx --version` output (`runx-cli 0.11.1`), and the full observation log.
