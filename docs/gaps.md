# Coverage & gaps {#coverage--gaps}


What this reference covers, and — more usefully — what a maintainer would still have to fix in the source for the documentation to be complete. Counts are computed from the pinned godoc snapshot, not estimated.


## Coverage {#coverage}


- **709 public APIs documented**: 318 package-level functions, 39 types, 352 methods across `assert`, `require`, `mock`, `suite`, and `http`.
- Every exported function and type in the public packages carries a doc comment in source (0 undocumented functions, 0 undocumented types in the snapshot) — testify's comment discipline at the declaration level is genuinely good.
- The `assert` → `require` relationship is fully visible: both packages are documented side by side, so the reader can see that `require` mirrors `assert` (153 vs 158 functions) with `FailNow` semantics.


## Gaps a maintainer would care about {#gaps-a-maintainer-would-care-about}


1. **The root package documents nothing.** `github.com/stretchr/testify` itself exports no API and its package page is a stub; a reader landing there gets no map of the sub-packages. This site compensates with the overview table on the home page, but the fix belongs in `doc.go` upstream.

2. **Generated code is not marked as generated.** `require` is produced from `assert` by the generator in `_codegen`, but neither package's doc comments say so. A reader comparing near-identical entries cannot tell which side is the source of truth, and a contributor may patch the generated side. One sentence in each package comment would fix it.

3. **Suite lifecycle hooks are conventions, not contracts.** `suite` documents 13 types and only 1 function; the actual programming model — `SetupSuite`, `TearDownTest`, and friends — is a set of optional interfaces a suite struct may implement, described in the README's prose rather than in the godoc of the interfaces themselves. The reference makes the interfaces findable; it cannot invent the missing lifecycle documentation.

4. **Examples do not survive into the reference.** The packages ship extensive `Example…` functions in their test files, but they are not attached to the symbols they demonstrate in the snapshot, so this site — like every godoc-derived reference — shows signatures and prose without runnable usage for most of the 709 entries. Wiring examples to symbols is the single highest-value documentation improvement available upstream.

5. **The `http` package is nearly invisible.** Two types and four methods, no package-level guidance on when to use it over `net/http/httptest`. It is documented here for completeness; upstream it reads as an afterthought and probably should either grow a real package comment or be explicitly deprecated in favour of the standard library.

6. **Failure-output behaviour is described inconsistently.** Some `assert` functions document exactly what is printed on failure (including the `msgAndArgs` convention); others with identical mechanics say nothing. Because `require` inherits the same comments by generation, the inconsistency appears twice.
