# How not to `rm` yourself

The [`rm`](http://en.wikipedia.org/wiki/Rm_\(Unix\)) command is inherently dangerous and should not be used directly. It can at worst let you accidentally remove **everything**. Here's how you can protect *you* from yourself.


## Use [`trash-cli`](https://github.com/sindresorhus/trash-cli)

The `trash-cli` command-line app will move stuff to the trash instead of permanently deleting it:

```
$ npm install --global trash-cli
```

```
$ trash unicorn.png rainbow.png
```

*Works on macOS, Linux, Windows. Requires [Node.js](http://nodejs.org).*


## Safeguard `rm`

Even though you don't use `rm` directly, external scripts most likely will. There are some things you can do to safeguard this:

- Alias `rm` to its interactive mode `rm -i`. Just doing this step is not enough as `-f` overrides `-i`.

	If you only want to alias `rm` in your interactive shell (and not in scripts), just add `alias rm='rm -i'` to your `.bashrc` or `.zshrc`.

	If you want to force scripts to use `rm -i` as well, follow these steps depending on which shell you're using:

	**bash**:
	- Add `alias rm='rm -i'` to your `.bashrc`.
	- Create a file called `.bashenv` in your home directory with `shopt -s expand_aliases` and `source .bashrc`.
	- In your `.bashrc`, add `export BASH_ENV='~/.bashenv'`.

	**zsh**:
	If you use zsh and want `rm` to be aliased in bash scripts, zsh scripts *and* your own interactive z shell, we have to jump through some more hoops:
	- Create a file called `.common_profile` in your home directory with `alias rm='rm -i'`
	- Create a file called `.bashenv` in your home directory with `source ~/.common_profile` and `shopt -s expand_aliases`.
	- Create a file called `.zshenv` in your home directory alongside `.bashenv` and add `source ~/.common_profile`.
	- Finally, in your `.zshrc` add `source ~/.common_profile` and `export BASH_ENV='~/.bashenv'`. Your `.common_profile`, `.bashenv`, `.zshenv` and `.zshrc` should end up looking like [this](https://gist.github.com/andbroby/958c6b4259290d4c884c).

- Install `coreutils` which includes a newer version of `rm` with the flag `--preserve-root` which is enabled by default and will prevent you from removing root.
	macOS: `brew install coreutils`
	Linux: *Included by default.*

	With this version of `rm` you can also choose to switch from `alias rm='rm -i'` to `alias rm='rm -I'` which is similar:

	> -I   prompt once before removing more than three files, or when removing recursively. Less intrusive than -i, while still giving protection against most mistakes.

- Install [`safe-rm`](https://launchpad.net/safe-rm) which will let you set off-limits directories.

- ZSH users can also do the following:
	- Put `unsetopt RM_STAR_SILENT` in your .zshrc, which will make it ask you before executing `rm` with a star `rm folder/*`.

	- Put `setopt RM_STAR_WAIT` in your .zshrc, which will make it wait 10 seconds until executing `rm` with a star `rm folder/*`.

- **Always backup your system.**
