# Set environment variables

> [Environment variables](http://en.wikipedia.org/wiki/Environment_variable) are a set of dynamic named values that can affect the way running processes will behave on a computer.


## OS X and Linux

1. Find out if you're using Bash or ZSH by running the command `echo $SHELL` in your Terminal.

2. Depending on if you're using Bash or ZSH check if `~/.bashrc` or `~/.zshrc` exists by running `open ~/.bashrc` or `open ~/.zshrc`. You can create it with `touch ~/.bashrc` or `touch ~/.zshrc` if it doesn't already exist. Then open it with `open ~/.bashrc` or `open ~/.zshrc`.

3. You can add an environment variable using the following syntax `export FOO='bar'` in the opened file. This will add the environment variable `FOO` with the value of `bar`.

*The tilde character `~` means your home folder. On my Mac `~` would translate into `/Users/sindresorhus`, on Linux distros `~` would translate into `/home/sindresorhus`.*


## Windows

1. Right-click on the Computer icon on your desktop or start-menu and choose the Properties menu item.

2. In the new `System` window click on `Advanced system settings`.

3. In the new `System Properties` window click the `Advanced` tab and then the `Environment Variables...` button.

4. Click the first `New...` button.

5. In the `New User Variable` box you can add the environment variable and value.
