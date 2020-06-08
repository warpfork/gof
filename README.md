gof
===

**Go F**reely is a simple bash script to set up a project-local GOPATH environment.

There have been many iterations of the "how do we make GOPATH not an impediment to sanity" wrapper scripts.  This is not the first, but it is the most recent, the most complete, and has been burning in without issues on my personal PATH for months now.  And unlike most previous shots at this, it has the venerable property of not requiring you add it to the project repo in order for it to work.

If you have to work with Go... ┐(￣ー￣)┌
gof.

_Is `gof` still relevant with the introduction of "go modules"?_

Well, that's up to you to decide.  But, since `gof` works both before and after the introduction of `go mod`, and works the same way before and after, unobtrusively...
_and_ still composes just fine with any versioning you want...?
I'd say it might still be relevant, yeah.


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


Integration
-----------

If you have other tools which invoke `go`, and you want them to use `gof`, it's easy.

The simplest thing to do is invoke via gof: `gof - thetool`.  This is an easy
way to use e.g. `dep` or other tools.

A more heavy-handed option for other tools that will invoke `go` is to actually
map `go` *into* calling `gof`.  We have scripts in the `ext/gof-universal`
directory which can help with this.  (This tactic is great for IDEs.)


Fork it
-------

Don't like something about `gof`?  Think it's too opinionated?

Fork it!

The great thing about `gof` is you can use it without adding the script nor persisting
any of its configuration to git, so you can keep your own fork that does whatever you want,
and it can be your little productivity-boosting secret.

:heart:
