# How not to `rm` yourself

The [`rm`](http://en.wikipedia.org/wiki/Rm_\(Unix\)) command is inherently dangerous and should not be used directly. It can at worst let you accidentally remove **everything**. Here's how you can protect *you* from yourself.


## Use [`trash`](https://github.com/sindresorhus/trash)

The `trash` command-line app will move stuff to the trash instead of permanently deleting it. You should not alias `rm` to `trash` as it will break external scripts relying on the behavior of `rm`. Instead use it directly:

```sh
$ npm install --global trash
```

```sh
$ trash unicorn.png rainbow.png
```

*Works on OS X, Linux, Windows. Requires [Node.js](http://nodejs.org).*


## Safeguard `rm`

Even though you don't use `rm` directly, external scripts most likely will. There are some things you can do to safeguard this:

- Alias `rm` to its interactive mode `rm -i` and set `shopt -s expand_aliases` in your `$BASH_ENV`. This will force you to step through what it's trying to delete.

- Install `coreutils` which includes a newer version of `rm` with the flag `--preserve-root` which is enabled by default and will prevent you from removing root.
	OS X: `brew install coreutils`
	Linux: `apt-get install coreutils`

	With this version of `rm` you can also choose to switch from `alias rm='rm -i'` to `alias rm='rm -I'` which is similar:

	> -I   prompt once before removing more than three files, or when removing recursively. Less intrusive than -i, while still giving protection against most mistakes.

- Install [`safe-rm`](https://launchpad.net/safe-rm) which will let you set off-limits directories.

- ZSH users can also do the following:
	- Put `unsetopt RM_STAR_SILENT` in your .zshrc, which will make it ask you before executing `rm` with a star `rm folder/*`.

	- Put `setopt RM_STAR_WAIT` in your .zshrc, which will make it wait 10 seconds until executing `rm` with a star `rm folder/*`.

- **Always backup your system.**
