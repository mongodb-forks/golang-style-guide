## 2025-02-10

- First version of this fork.
- Recommend the new atomic types like `atomic.Bool` instead of the `go.uber.org/atomic` package. The
  Uber package predates the new types added in Go 1.19. The new stdlib types provide more or less
  the same functionality as Uber's package.
- Replaced recommendation to use `golint` with `revive`, as `golint` is long since deprecated.
- Replaced recommendation to use `goimports` with `gofumpt`.
- Added a recommendation to use `gopls` in general, and specifically to configure your editor to use
  it to update imports.
