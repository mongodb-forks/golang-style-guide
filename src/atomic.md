<!-- This entirely replaces Uber's version of this file, which recommends the use of
go.uber.org/atomic. That package predates the new types added in Go 1.19. The new stdlib types
provide more or less the same functionality as Uber's package. -->

# Use the New Types in sync/atomic

In the past, the [sync/atomic] package was implemented entirely in terms of functions like
`atomic.AddInt64`, which were awkward to use and made it easy to accidentally access the underlying
value non-atomically..

Since Go 1.19, the [sync/atomic] package provides atomic types like `atomic.Bool` and
`atomic.Int64`, which provide a much safer API for atomic operations, making it impossible to read
or modify them with a non-atomic operation.

<!--

TODO: It'd be nice to have a shared library that provided a typed atomic value instead of having
people use `atomic.Value`. We've written such a thing for Mongosync. See
https://github.com/10gen/mongosync/blob/main/mongo-go/msync/typed_atomic.go for details.

-->

<table>
<thead><tr><th>Bad</th><th>Good</th></tr></thead>
<tbody>
<tr><td>

```go
type foo struct {
  running atomic.Int32  // atomic
}

func (f* foo) start() {
  if atomic.SwapInt32(&f.running, 1) == 1 {
     // already running…
     return
  }
  // start the Foo
}

func (f *foo) isRunning() bool {
  return f.running == 1  // race!
}
```

</td><td>

```go
type foo struct {
  running atomic.Bool
}

func (f *foo) start() {
  if f.running.Swap(true) {
     // already running…
     return
  }
  // start the Foo
}

func (f *foo) isRunning() bool {
  return f.running.Load()
}
```

</td></tr>
</tbody></table>
