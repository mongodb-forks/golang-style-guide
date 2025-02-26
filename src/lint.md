# Linting

More importantly than any "blessed" set of linters, lint consistently across a
codebase.

We recommend using the following linters at a minimum, because we feel that they
help to catch the most common issues and also establish a high bar for code
quality without being unnecessarily prescriptive:

- [errcheck] to ensure that errors are handled
- [gofumpt] to format code and manage imports
- [govet] to analyze code for common mistakes
- [revive] to point out common style mistakes
- [staticcheck] to do various static analysis checks

  [errcheck]: https://github.com/kisielk/errcheck
  [gofumpt]: https://github.com/mvdan/gofumpt
  [govet]: https://pkg.go.dev/cmd/vet
  [revive]: https://github.com/mgechev/revive
  [staticcheck]: https://staticcheck.dev

## Additional Recommended Linters

We recommend consider some or all the following linters in addition to those listed above. Note that
many of these linters have a variety of configuration options. We encourage you to read each
linter's documentation and consider how you'd like to configure them when you adopt them.

### Code Complexity and Quality

- [cyclop] to check code's cyclomatic complexity, which is a heuristic evaluation of "how hard is
  this code to understand" based on things like how many statements a function has, how many
  conditional it uses, etc.
- [funlen] to check a function's length in lines and statements.
- [gocognit] to check code's cognitive complexity. This is similar to cognitive complexity but uses
  a different heuristic.
- [gocritic] is a style checker along the lines of `govet` and `revive`. Notably, this linter allows
  you to use [ruleguard]. See the [Ruleguard] section for more details.
- [maintidx] measures the maintainability index of functions. Again, this is imilar to the
  cyclomatic and cognitive complexity heuristics.
- [nestif] detects `if` nesting past a given level.

  [cyclop]: https://github.com/bkielbasa/cyclop
  [funlen]: https://github.com/ultraware/funlen
  [gocognit]: https://github.com/uudashr/gocognit
  [gocritic]: https://go-critic.com/
  [maintidx]: https://github.com/uudashr/gocognit
  [nestif]: https://github.com/nakabonne/nestif
  [ruleguard]: https://github.com/quasilyte/go-ruleguard

### Error Types, Messages, and Error Handling

- [errname] checks that error types and names follow Golang standards.
- [errorlint] checks for code that embeds errors as strings instead of wrapping them, as well as
  code that uses type assertions instead of `errors.As` or `errors.Is`.
- [nilnesserr] checks for incorrect error handling corner cases, for example checking if `err2 !=
  nil` and then returning `err` instead of `err2`.

  [errname]: https://github.com/Antonboom/errname
  [errorlint]: https://github.com/polyfloyd/go-errorlint
  [nilnesserr]: https://github.com/alingse/nilnesserr

### Imports

- [depguard] allows you to forbid imports of specific packages, either entirely, or only in certain
  files.
- [gci] enforces import order and general formatting of the `imports` section. This goes a bit
  beyond what `gopls` does in terms of formatting imports.
- [importas] enforces the use of the same alias everywhere a given package is aliased. In other
  words, it requires to always alias `github.com/google/uuid` as something like `guuid`, rather than
  using `guuid` in one package and `u` in another.

  [depguard]: https://github.com/OpenPeeDeeP/depguard
  [gci]: https://github.com/daixiang0/gci
  [importas]: https://github.com/julz/importas

## Spelling and Grammar

- [dupword] checks for duplicate words in comments or strings like "failed because the the server
  returned an error".
- [godot] requires all comments to end in a period.
- [misspell] checks for commonly misspelled English words.

  [dupword]: https://github.com/Abirdcfly/dupword
  [godot]: https://github.com/tetafro/godot
  [misspell]: https://github.com/client9/misspell

### Code Quality and Cleanup

- [copyloopvar] finds places where loop variables are copied, like `i := i`. This is no longer
  necessary as of Go 1.22.
- [exhaustruct] requires that all fields of a struct be initialized when a struct is created.
- [exptostd] checks for use of function in `golang.org/x/exp` packages that can be replaced by
  functions from the standard library.
- [gocheckcompilerdirectives] checks that Go compiler directive comments, like `//go:build ...`, are
  valid.
- [iface] detects unused interfaces, multiple identical interfaces, and functions which return
  interfaces but always return the same concrete implementation type.
- [ineffassign] detects when a variable is assigned a value but that value is never used, for
  example if you reassign to a variable but never use the first value.
- [intrange] finds loops where you can use the `for i := 10` integer range feature added in Go 1.22.
- [nolintlint] finds `//nolint` comments for `golangci-lint` that are ill-formed, don't have an
  exaplanatory comment, or are applied to code that doesn't trigger the disabled linter(s).
- [predeclared] finds code that shadow predeclared Go identifiers like a function named `copy`.
- [recvcheck] checks that all receivers for a type are pointers or non-pointers.
  - Note that if you use this you will almost certainly want to exempt `MarshalBSON` and
    `UnmarshalBSON` methods from this linter.
- [testifylint] checks for various issues when using the [testify] test packages.
- [unconvert] finds unnecessary type conversions.
- [unparam] finds unused function parameters.
- [unused] finds unused constants, variables, functions, and types.
- [usestdlibvars] finds places where you can use stdlib vars like `http.StatusOK` instead of `200`.
- [usetesting] finds places where you can using `testing` package helpers like `t.TempDir` instead
  of `os.TempDir`.

  [copyloopvar]: https://github.com/karamaru-alpha/copyloopvar
  [exhaustruct]: https://github.com/GaijinEntertainment/go-exhaustruct
  [exptostd]: https://github.com/ldez/exptostd
  [gocheckcompilerdirectives]: https://github.com/leighmcculloch/gocheckcompilerdirectives
  [iface]: https://github.com/uudashr/iface
  [ineffassign]: https://github.com/gordonklaus/ineffassign
  [intrange]: https://github.com/ckaznocha/intrange
  [nolintlint]: https://github.com/golangci/golangci-lint/tree/master/pkg/golinters/nolintlint/internal
  [predeclared]: https://github.com/nishanths/predeclared
  [recvcheck]: https://github.com/raeperd/recvcheck
  [testifylint]: https://github.com/Antonboom/testifylint
  [testify]: https://github.com/stretchr/testify
  [unconvert]: https://github.com/mdempsky/unconvert
  [unparam]: https://github.com/mvdan/unparam
  [unused]: https://github.com/dominikh/go-tools/tree/master/unused
  [usestdlibvars]: https://github.com/sashamelentyev/usestdlibvars
  [usetesting]: https://github.com/ldez/usetesting

### Ruleguard

The [gocritic] linter allows you to use [ruleguard]. Ruleguard is a tool that lets you write
declarative rules that your codebase is checked against. This is a very flexible tool that allows
you to write checks for things that cannot be done with any existing linter.

For example, you could write rules to:

- forbid the use of specific generic types.
- forbid specific functions from certain packages.
- require that all context cancellations, deadlines, and timeouts have a cause, among many .

## Lint Runners

For projects which use Bazel, you should use [nogo] instead of [golangci-lint], as [golangci-lint]
does not work well with Bazel's sandboxing.

Otherwise, we recommend [golangci-lint] as the go-to lint runner for Go code, largely due
to its performance in larger codebases and ability to configure and use many
canonical linters at once. This repo has an example [.golangci.yml] config file
with recommended minimal linters and settings.

There is also a [.golangci-maximal.yml] file with all the additional linters enabled.

golangci-lint has [various linters] available for use. The above linters are
recommended as a base set, and we encourage teams to add any additional linters
that make sense for their projects.

  [nogo]: https://github.com/bazel-contrib/rules_go/blob/master/go/nogo.rst
  [golangci-lint]: https://github.com/golangci/golangci-lint
  [.golangci.yml]: https://github.com/uber-go/guide/blob/master/.golangci.yml
  [various linters]: https://golangci-lint.run/usage/linters/
