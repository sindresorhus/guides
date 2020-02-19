# Install `npm` packages globally without sudo on macOS and Linux

`npm` installs packages locally within your projects by default. You can also install packages globally (e.g. `npm install -g <package>`) (useful for command-line apps). However the downside of this is that you need to be root (or use `sudo`) to be able to install globally.

Here is a way to install packages globally for a given user.

###### 1. Create a directory for global packages

```sh
mkdir "${HOME}/.npm-packages"
```

###### 2. Tell `npm` where to store globally installed packages

```sh
npm config set prefix "${HOME}/.npm-packages"
```

###### 3. Ensure `npm` will find installed binaries and man pages

Add the following to your `.bashrc`/`.zshrc`:

```sh
NPM_PACKAGES="${HOME}/.npm-packages"

export PATH="$PATH:$NPM_PACKAGES/bin"

# Preserve MANPATH if you already defined it somewhere in your config.
# Otherwise, fall back to `manpath` so we can inherit from `/etc/manpath`.
export MANPATH="${MANPATH-$(manpath)}:$NPM_PACKAGES/share/man"
```

If you're using `fish`, add the following to `~/.config/fish/config.fish`:

```sh
set NPM_PACKAGES "$HOME/.npm-packages"

set PATH $PATH $NPM_PACKAGES/bin

set MANPATH $NPM_PACKAGES/share/man $MANPATH  
```

If you have erased your MANPATH by mistake, you can restore it by running `set -Ux MANPATH (manpath -g) $MANPATH` once. Do not put this command in your `config.fish`.

---

Check out [`npm-g_nosudo`](https://github.com/glenpike/npm-g_nosudo) for doing the above steps automagically

---

NOTE: If you are running macOS, the `.bashrc` file may not yet exist, and the terminal will be obtaining its environment parameters from another file, such as `.profile` or `.bash_profile`. These files also reside in the user's home folder. In this case, simply adding the following line to them will instruct Terminal to also load the `.bashrc` file:

```sh
source ~/.bashrc
```

---

See also: `npm`'s documentation on
["Fixing `npm` permissions"](https://docs.npmjs.com/getting-started/fixing-npm-permissions).
