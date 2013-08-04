# Install packages globally on Linux without sudo

npm installs packages locally within each of your projects. Additionally, you
can also install packages globally (e.g. `-g` switch of npm). However
the downside of this is that you need to be root (or use `sudo`) to be
able to install globally. 
Here is a way to install packages globally for a given user.

1. Create a directory for your global packages
```bash 
mkdir ~/.npm-packages
```

2. Reference this directory for future usage in your `.bashrc`/`.zshrc`:
```bash
NPM_PACKAGES="~/.npm-packages"
```

3. Indicate to `npm` where to store your globally installed package. In
   your `~/.npmrc` file add:
```
prefix=~/.npm-packages
```

4. Ensure `node` will find them. Add the following to your
   `.bashrc`/`.zshrc`:
```bash
NODE_PATH="$NPM_PACKAGES/lib/node_modules:$NODE_PATH"
```

5. Ensure you'll find installed binaries and man pages. Add the following to your
   `.bashrc`/`.zshrc`:
```bash
PATH="$NPM_PACKAGES/bin:$PATH"
# Unset manpath so we can inherit from /etc/manpath via the `manpath`
# command
unset MANPATH  # delete if you already modified MANPATH elsewhere in
your config
MANPATH="$NPM_PACKAGES/share/man:$(manpath)"
```

Inspired from this [answer on
StackOverflow](http://stackoverflow.com/a/13021677).

