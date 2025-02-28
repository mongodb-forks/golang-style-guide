# Introduction

Styles are the conventions that govern our code. The term style is a bit of a
misnomer, since these conventions cover far more than just source file
formatting—gofumpt handles that for us.

The goal of this guide is to manage this complexity by describing in detail the
Dos and Don'ts of writing Go code at Uber. These rules exist to keep the code
base manageable while still allowing engineers to use Go language features
productively.

This guide was originally created by [Prashant Varanasi] and [Simon Newton] as
a way to bring some colleagues up to speed with using Go. Over the years it has
been amended based on feedback from others.

  [Prashant Varanasi]: https://github.com/prashantv
  [Simon Newton]: https://github.com/nomis52

This documents idiomatic conventions in Go code that we follow at Uber. A lot
of these are general guidelines for Go, while others extend upon external
resources:

1. [Effective Go](https://go.dev/doc/effective_go)
2. [Go Common Mistakes](https://go.dev/wiki/CommonMistakes)
3. [Go Code Review Comments](https://go.dev/wiki/CodeReviewComments)

We aim for the code samples to be accurate for the two most recent minor versions
of Go [releases](https://go.dev/doc/devel/release).

You should set up your editor to integrate with Go's LSP server, [gopls].

  [gopls]: https://github.com/golang/tools/tree/master/gopls

All code should be error-free when run through `revive` and `go vet`. We
recommend setting up your editor to:

- Use `gopls` to update your code's imports automatically on save
- Run `gofumpt` on save
- Run `revive` and `go vet` to check for errors

Note that you may wish to use [golangci-lint] or Bazel's [nogo] to run `gofumpt`, `revive`, and `go
vet` instead of running each one separately.

  [golangci-lint]: https://golangci-lint.run/
  [nogo]: https://github.com/bazel-contrib/rules_go/blob/master/go/nogo.rst

You can find information in editor support for Go tools here:
<https://go.dev/wiki/IDEsAndTextEditorPlugins>

## MongoDB Style

This style guide is a fork of the [Uber Style Guide](https://github.com/uber-go/guide) maintained by
MongoDB. It is largely the same as Uber's. All changes specific to MongoDB are noted in the
[CHANGELOG-MongoDB.md](./CHANGELOG-MongoDB.md) file. In addition, we have used HTML comments to make
notes in most places where we have made changes from the Uber version.
