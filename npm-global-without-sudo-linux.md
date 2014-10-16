# Install npm packages globally on Linux without sudo

npm installs packages locally within each of your projects by default. You
can also install packages globally (e.g. `npm install -g <package>`). However
the downside of this is that you need to be root (or use `sudo`) to be
able to install globally.

Here is a way to install packages globally for a given user.

1. Create a directory for your global packages

```sh
mkdir "${HOME}/.npm-packages"
```

2. Reference this directory for future usage in your `.bashrc`/`.zshrc`:

```sh
NPM_PACKAGES="${HOME}/.npm-packages"
```

3. Indicate to `npm` where to store your globally installed package. In
   your `$HOME/.npmrc` file add:

```sh
prefix=${HOME}/.npm-packages
```

4. Ensure `node` will find them. Add the following to your
   `.bashrc`/`.zshrc`:

```sh
NODE_PATH="$NPM_PACKAGES/lib/node_modules:$NODE_PATH"
```

5. Ensure you'll find installed binaries and man pages. Add the following to your
   `.bashrc`/`.zshrc`:

```sh
PATH="$NPM_PACKAGES/bin:$PATH"
# Unset manpath so we can inherit from /etc/manpath via the `manpath`
# command
unset MANPATH  # delete if you already modified MANPATH elsewhere in your config
MANPATH="$NPM_PACKAGES/share/man:$(manpath)"
```

Inspired from this [answer on StackOverflow](http://stackoverflow.com/a/13021677).

There is a script in the https://github.com/glenpike/npm-g_nosudo repository to automate fixing existing global npm package installations by moving these to the ~/.npm-packages directory and setting the appropriate variables above.
