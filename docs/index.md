# Testify API Reference {#testify-api-reference}


A complete, navigable API reference for **[stretchr/testify](https://github.com/stretchr/testify)** — the most widely used assertion toolkit for Go — generated from source with [Sourcey](https://sourcey.com) and pinned to an exact upstream commit so the text on this site cannot drift away from the code it describes.

- **Upstream repository:** https://github.com/stretchr/testify
- **Pinned commit:** `87a7b9d57689f6579db2da795ab8deeab29cb724` (2026-09-24)
- **License:** MIT (see the `LICENSE` file in the upstream tree)
- **Generator:** Sourcey 3.9.5, `godoc` adapter in snapshot mode
- **Coverage:** 6 public packages, **709 documented public APIs** (functions, types, and methods)


## Packages {#packages}


| Package | What it does | Documented APIs |
| --- | --- | --- |
| `assert` | Assertions that return `bool` and log failures without stopping the test | 158 functions, 11 types, 157 methods |
| `require` | The same assertions, but they call `t.FailNow()` on failure | 153 functions, 6 types, 152 methods |
| `mock` | Mock objects: expectations, call recording, argument matchers | 6 functions, 7 types, 32 methods |
| `suite` | Test suites with setup/teardown lifecycle hooks | 1 function, 13 types, 7 methods |
| `http` | Small HTTP test helpers (test round-tripper and friends) | 2 types, 4 methods |
| `testify` (root) | Package landing page only — no exported API | 0 |


## Why this site exists {#why-this-site-exists}


Testify's canonical documentation is its README plus `pkg.go.dev`. The README is a tutorial, not a reference: it shows the popular assertions and leaves the long tail — format-string variants, the `assert`/`require` generation relationship, mock argument matchers, suite lifecycle interfaces — to be discovered from source. This site renders the whole public surface from the source itself, with navigation, search, and per-symbol pages, so a reader can answer "does testify have an assertion for X, and what exactly does it return?" without cloning the repository.

See **Provenance** for exactly how this site was produced and how to reproduce it, and **Coverage & gaps** for what a maintainer would still need to fix in the source comments themselves.
