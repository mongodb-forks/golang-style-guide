# 2025-01-31

- Recommend the new atomic types like `atomic.Bool` instead of the `go.uber.org/atomic` package.
- Replace recommendation to use `golint` with `revive`, as `golint` is long since deprecated.
- Replace recommendation to use `goimports` with `gofumpt`. Also fixed a reference to `gofmt` in the
  intro to use `gofumpt` instead.
- Added a recommendation to use `gopls` in general, and specifically to configure your editor to use
  it to update imports.