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

## Lint Runners

For projects which use Bazel, you should use [nogo] instead of [golangci-lint], as [golangci-lint]
does not work well with Bazel's sandboxing.

Otherwise, we recommend [golangci-lint] as the go-to lint runner for Go code, largely due
to its performance in larger codebases and ability to configure and use many
canonical linters at once. This repo has an example [.golangci.yml] config file
with recommended linters and settings.

golangci-lint has [various linters] available for use. The above linters are
recommended as a base set, and we encourage teams to add any additional linters
that make sense for their projects.

  [nogo]: https://github.com/bazel-contrib/rules_go/blob/master/go/nogo.rst
  [golangci-lint]: https://github.com/golangci/golangci-lint
  [.golangci.yml]: https://github.com/uber-go/guide/blob/master/.golangci.yml
  [various linters]: https://golangci-lint.run/usage/linters/
