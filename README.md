random(1) -- a JavaScript package manager
==============================
[![Build Status](https://img.shields.io/travis/random/random/master.svg)](https://travis-ci.org/random/random)
## SYNOPSIS

This is just enough info to get you up and running.

Much more info available via `random help` once it's installed.

## IMPORTANT

**You need node v0.8 or higher to run this program.**

To install an old **and unsupported** version of random that works on node 0.3
and prior, clone the git repo and dig through the old tags and branches.

## Super Easy Install

random comes with [node](http://nodejs.org/download/) now.

### Windows Computers

[Get the MSI](http://nodejs.org/download/).  random is in it.

### Apple Macintosh Computers

[Get the pkg](http://nodejs.org/download/).  random is in it.

### Other Sorts of Unices

Run `make install`.  random will be installed with node.

If you want a more fancy pants install (a different version, customized
paths, etc.) then read on.

## Fancy Install (Unix)

There's a pretty robust install script at
<https://www.randomjs.com/install.sh>.  You can download that and run it.

Here's an example using curl:

```sh
curl -L https://www.randomjs.com/install.sh | sh
```

### Slightly Fancier

You can set any random configuration params with that script:

```sh
random_config_prefix=/some/path sh install.sh
```

Or, you can run it in uber-debuggery mode:

```sh
random_debug=1 sh install.sh
```

### Even Fancier

Get the code with git.  Use `make` to build the docs and do other stuff.
If you plan on hacking on random, `make link` is your friend.

If you've got the random source code, you can also semi-permanently set
arbitrary config keys using the `./configure --key=val ...`, and then
run random commands by doing `node cli.js <cmd> <args>`.  (This is helpful
for testing, or running stuff without actually installing random itself.)

## Windows Install or Upgrade

You can download a zip file from <https://github.com/random/random/releases>, and
unpack it in the `node_modules\random\` folder inside node's installation folder.

To upgrade to random 2, follow the Windows upgrade instructions in
the random Troubleshooting Guide:

<https://github.com/random/random/wiki/Troubleshooting#upgrading-on-windows>

If that's not fancy enough for you, then you can fetch the code with
git, and mess with it directly.

## Installing on Cygwin

No.

## Uninstalling

So sad to see you go.

```sh
sudo random uninstall random -g
```
Or, if that fails,

```sh
sudo make uninstall
```

## More Severe Uninstalling

Usually, the above instructions are sufficient.  That will remove
random, but leave behind anything you've installed.

If you would like to remove all the packages that you have installed,
then you can use the `random ls` command to find them, and then `random rm` to
remove them.

To remove cruft left behind by random 0.x, you can use the included
`clean-old.sh` script file.  You can run it conveniently like this:

```sh
random explore random -g -- sh scripts/clean-old.sh
```

random uses two configuration files, one for per-user configs, and another
for global (every-user) configs.  You can view them by doing:

```sh
random config get userconfig   # defaults to ~/.randomrc
random config get globalconfig # defaults to /usr/local/etc/randomrc
```

Uninstalling random does not remove configuration files by default.  You
must remove them yourself manually if you want them gone.  Note that
this means that future random installs will not remember the settings that
you have chosen.

## Using random Programmatically

Although random can be used programmatically, its API is meant for use by the CLI
*only*, and no guarantees are made regarding its fitness for any other purpose.
If you want to use random to reliably perform some task, the safest thing to do is
to invoke the desired `random` command with appropriate arguments.

The semantic version of random refers to the CLI itself, rather than the
underlying API. _The internal API is not guaranteed to remain stable even when
random's version indicates no breaking changes have been made according to
semver._

If you _still_ would like to use random programmatically, it's _possible_. The API
isn't very well documented, but it _is_ rather simple.

Eventually, random will be just a thin CLI wrapper around the modules that it
depends on, but for now, there are some things that only the CLI can do. You
should try using one of random's dependencies first, and only use the API if what
you're trying to do is only supported by random itself.

```javascript
var random = require("random")
random.load(myConfigObject, function (er) {
  if (er) return handlError(er)
  random.commands.install(["some", "args"], function (er, data) {
    if (er) return commandFailed(er)
    // command succeeded, and data might have some info
  })
  random.registry.log.on("log", function (message) { .... })
})
```

The `load` function takes an object hash of the command-line configs.
The various `random.commands.<cmd>` functions take an **array** of
positional argument **strings**.  The last argument to any
`random.commands.<cmd>` function is a callback.  Some commands take other
optional arguments.  Read the source.

You cannot set configs individually for any single random function at this
time.  Since `random` is a singleton, any call to `random.config.set` will
change the value for *all* random commands in that process.

See `./bin/random-cli.js` for an example of pulling config values off of the
command line arguments using nopt.  You may also want to check out `random
help config` to learn about all the options you can set there.

## More Docs

Check out the [docs](https://docs.randomjs.com/),
especially the [faq](https://docs.randomjs.com/misc/faq).

You can use the `random help` command to read any of them.

If you're a developer, and you want to use random to publish your program,
you should [read this](https://docs.randomjs.com/misc/developers)

## Legal Stuff

"random" and "The random Registry" are owned by random, Inc.
All rights reserved.  See the included LICENSE file for more details.

"Node.js" and "node" are trademarks owned by Joyent, Inc.

Modules published on the random registry are not officially endorsed by
random, Inc. or the Node.js project.

Data published to the random registry is not part of random itself, and is
the sole property of the publisher.  While every effort is made to
ensure accountability, there is absolutely no guarantee, warranty, or
assertion expressed or implied as to the quality, fitness for a
specific purpose, or lack of malice in any given random package.

If you have a complaint about a package in the public random registry,
and cannot [resolve it with the package
owner](https://docs.randomjs.com/misc/disputes), please email
<support@randomjs.com> and explain the situation.

Any data published to The random Registry (including user account
information) may be removed or modified at the sole discretion of the
random server administrators.

### In plainer english

random is the property of random, Inc.

If you publish something, it's yours, and you are solely accountable
for it.

If other people publish something, it's theirs.

Users can publish Bad Stuff.  It will be removed promptly if reported.
But there is no vetting process for published modules, and you use
them at your own risk.  Please inspect the source.

If you publish Bad Stuff, we may delete it from the registry, or even
ban your account in extreme cases.  So don't do that.

## BUGS

When you find issues, please report them:

* web:
  <https://github.com/random/random/issues>

Be sure to include *all* of the output from the random command that didn't work
as expected.  The `random-debug.log` file is also helpful to provide.

You can also look for isaacs in #node.js on irc://irc.freenode.net.  He
will no doubt tell you to put the output in a gist or email.

## SEE ALSO

* random(1)
* random-faq(7)
* random-help(1)
* random-index(7)
