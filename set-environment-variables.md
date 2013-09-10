# Set environment variables

> [Environment variables](http://en.wikipedia.org/wiki/Environment_variable) are a set of dynamic named values that can affect the way running processes will behave on a computer.

> They are part of the operating environment in which a process runs. For example, a running process can query the value of the TEMP environment variable to discover a suitable location to store temporary files, or the HOME or USERPROFILE variable to find the directory structure owned by the user running the process.


## OS X

1. Find out if you're using Bash or ZSH by running the command `echo $SHELL` in your Terminal.

2. Depending on if you're using Bash or ZSH check if `~/.bashrc` or `~/.zshrc` exists by running `open ~/.bashrc`. Skip step 3 if it opens.

3. Create the file with `touch ~/.bashrc` or `touch ~/.zshrc` if it doesn't already exist. Then open it with `open ~/.bashrc` or `open ~/.zshrc`.

4. Add an environment variable using the following syntax `export FOO='bar'` at the end of the opened file. This will add an environment variable named `FOO` with the value of `bar`.

5. Now just restart your terminal or reload the profile with `source ~/.bashrc` or `source ~/.zshrc`.

*The tilde character `~` means your home folder and translates into `/Users/yourusername`.*


## Linux

1. Find out if you're using Bash or ZSH by running the command `echo $SHELL` in your Terminal.

2. Depending on if you're using Bash or ZSH check if `~/.bashrc` or `~/.zshrc` exists by running `xdg-open ~/.bashrc` or `xdg-open ~/.zshrc`. Skip step 3 if it opens.

3. Create the file with `touch ~/.bashrc` or `touch ~/.zshrc` if it doesn't already exist. Then open it with `xdg-open ~/.bashrc` or `xdg-open ~/.zshrc`.

4. Add an environment variable using the following syntax `export FOO='bar'` at the end of the opened file. This will add an environment variable named `FOO` with the value of `bar`.

5. Now just restart your terminal or reload the profile with `source ~/.bashrc` or `source ~/.zshrc`.

*The tilde character `~` means your home folder and translates into `/home/yourusername`.*


## Windows

### Windows 7 and 8

1. Open `cmd.exe`

2. Type `setx FOO bar`. This will add an environment variable named FOO with the value of bar.

### Alternative (without command line and for older Windows)

1. Right-click on the Computer icon on your desktop or start-menu and choose the Properties menu item.

2. In the new `System` window click on `Advanced system settings`.

3. In the new `System Properties` window click the `Advanced` tab and then the `Environment Variables...` button.

4. Click the first `New...` button.

5. In the `New User Variable` box you can add an environment variable name and value.
