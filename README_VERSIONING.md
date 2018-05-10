Dependency versioning with `gof`
--------------------------------

`gof` doesn't prescribe anything about how you manage dependencies.

`gof get -d` will work just like normal `go get`, putting the resulting source
into `.gopath/src`.

From there, do what you want.
Every approach out there is easier when you have project-scoped GOPATH.


### Vendoring?

Whether or not you vendor code, and whether or not you do it in the
`GO15VENDOREXPERIMENT` directory layout, is up to you.

You can disregard the Go vendoring experiment completely when using `gof`.
Libraries can be placed in `.gopath/src`, as per the norm with GOPATH.

Or, if you really want, you can use the `vendor/` dir too.  It's fine.


### Submodules

Git submodules are quite apt at tracking changes,
they're easy to use in the Go ecosystem since effectively everyone already uses git,
and they're vastly more efficient over time than vendoring.

Git submodules compose effortlessly with the `gof` project-local GOPATH.

Try using `gof get -d` and then just turning all the cloned repos into submodules;
it's a pretty nice life.
