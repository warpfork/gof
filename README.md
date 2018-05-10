gof
===

**Go F**reely is a simple bash script to set up a project-local GOPATH environment.

Usage
-----

### Setup

`gof` needs a tiny bit of configuration: the Go toolchain needs to know what the canonical,
public import URL is for the project, and so you need to tell `gof` that before we can get started.

```
gof --init your.project.import/url
```

### Examples

All `go` commands are the same, only called via `gof`:

```
gof get -d
gof test ./...
gof test ./... -count=1
gof install
gof env
```

Any other commands which need a GOPATH can be be run by prefixing them with `gof -`:

```
gof - bash -c 'echo "$GOPATH"'
```


Persistence
-----------

`gof` places a `.gopath` dir in your project and keeps everything there.

By default, a `.gopath/.gitignore` file will also be created, so you can use this
in git repos that you don't own very easily.

`gof` makes two symlinks:

- one in `.gopath/src/your.project.import/url`, which points back up to the root;
- one in `.gopath/self`, which points to the above link.

These links ensure the import path for your code is the same as it would be if we
were using a global GOPATH, and also provide a config hint for `gof`.


Implementation
--------------

In essense:

```
	# Export local gopath and gobin.
	export GOBIN="$PWD/bin/"
	export GOPATH="$PWD/.gopath"

	# Set PWD to the self path to give other tools the most normal ideas possible.
	cd "$GOPATH/src/$PKG/$DEEPER"

	# Use ALL GO COMMANDS as NORMAL.  You now have a project-local scoped gopath!  NBD.
	"$@"
```


Fork it
-------

Don't like something about `gof`?  Think it's too opinionated?

Fork it!

The great thing about `gof` is you can use it without adding the script nor persisting
any of its configuration to git, so you can keep your own fork that does whatever you want,
and it can be your little productivity-boosting secret.

:heart: