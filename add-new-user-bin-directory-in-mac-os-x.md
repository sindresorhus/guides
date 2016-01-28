#Add New User Bin Directory in Mac OS X

1. Create the Directory "Bin" in your home directory (~/Bin)
2. Create the file ".bash_profile" in your home directory if it doesn't exist.
3. Add the following two lines (the first line is just a comment):
        #Adding a bin in my user dir to PATH
        export PATH=$PATH:~/Bin

    `"~/Bin"` is now in your $PATH.

4. Put **ngrok** and your other executable files in your new and easy accessible binary directory `"~/Bin"` or as you may recognize as `"Harddisk/Users/YourName/Bin"`.

    You are now able to type ngrok in Terminal from anywhere instead of typing ./ngrok from you home directory only.
   

