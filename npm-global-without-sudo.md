# Install `npm` packages globally without sudo on OS X and Linux

`npm` installs packages locally within your projects by default. You can also install packages globally (e.g. `npm install -g <package>`) (useful for command-line apps). However the downside of this is that you need to be root (or use `sudo`) to be able to install globally.

Here is a way to install packages globally for a given user.

###### 1. Create a directory for globally packages

```sh
mkdir "${HOME}/.npm-packages"
```

###### 2. Indicate to `npm` where to store globally installed packages. In your `~/.npmrc` file add:

```sh
prefix=${HOME}/.npm-packages
```

###### 3. Ensure `npm` will find installed binaries and man pages. Add the following to your `.bashrc`/`.zshrc`:

```sh
NPM_PACKAGES="${HOME}/.npm-packages"

PATH="$NPM_PACKAGES/bin:$PATH"

# Unset manpath so we can inherit from /etc/manpath via the `manpath` command
unset MANPATH # delete if you already modified MANPATH elsewhere in your config
export MANPATH="$NPM_PACKAGES/share/man:$(manpath)"
```

-

Check out [`npm-g_nosudo`](https://github.com/glenpike/npm-g_nosudo) for doing the above steps automagically

-

NOTE: If you are running OS X, the `.bashrc` file may not yet exist, and the terminal will be obtaining its environment parameters from another file, such as `.profile` or `.bash_profile`. These files also reside in the user's home folder. In this case, simply adding the following line to them will instruct Terminal to also load the `.bashrc` file:

```sh
source ~/.bashrc
```

---
###### 4. Get and install the latest npm, which is 3.5.3 at the time of this writing. 
```
curl -L https://www.npmjs.org/install.sh | sh
```

---
See also: `npm`'s documentation on
["Fixing `npm` permissions"](https://docs.npmjs.com/getting-started/fixing-npm-permissions).

---
See also: how to 
[completely uninstall Node.js from Mac OS X](http://benznext.com/completely-uninstall-node-js-from-mac-os-x/)
