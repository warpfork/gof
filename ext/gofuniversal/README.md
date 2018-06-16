go->gof universal adapter
=========================

Use the `go` script in this directory as a universal adapter to working with `gof`.

Put this dir on the *front* your `$PATH`, so it takes precidence over the real `go` command:

```
export PATH=/abs/path/to/gofuniversal:$PATH
```

And now any tool that invokes `go` commands will be quietly convinced to use `gof`!

This works even if you're invoking a tool that invokes a tool that runs an IDE that
scripts a build that... etc, you get the idea: it works, no matter how much indirection.

Note that as usual, you'll need to `gof --init` in paths where you intend to work;
otherwise, `gof` will halt and inform you there's no initialized gopath.
