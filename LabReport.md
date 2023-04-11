In order to access a remote server through Visual Studio Code, we will follow these steps:

1) Download Visual Studio Code (if not already downloaded)

2) If you're using a non-Unix-based operating system (like Windows), download Git.

3) Access the server through a bash terminal in VSC.

We will now go through each of these steps in more depth:

1) 
Visual Studio Code can be downloaded through this link: https://code.visualstudio.com/download

Upon opening the program, you will see a screen like this:

![image](https://user-images.githubusercontent.com/130111715/231045057-e4e7d529-0f45-4af9-95b2-780470da94bb.png)

2)
Git for Windows can be downloaded through this link:https://git-scm.com/download/win

If you are on MacOS, Linux, or any other Unix-based OS, you can skip this step.

3)
Now, open Visual Studio Code and create a terminal by using *Ctrl* + *Shift* + *`*. You will now set your default terminal to the git bash you installed.
Open the command palette by clicking *Ctrl* + *Shift* + *P* and select *Git Bash* from the options. Now, simply click the *+* icon in the terminal. Notice that you are now using a git bash terminal:



You are now ready to remote connect to a server!

________________________________________________

You will now connect to your CSE 15L account:


Begin by typing *$ ssh cs15lsp23__@ieng6.ucsd.edu* into your bash terminal (replace the blank spaces with the letters associated with your account).

Upon doing this, you will be requested to enter your password. When you type it in, you will not see the the asterisks you usually see when
logging into an account. Don't worry, your password *is* being entered.

![image](https://user-images.githubusercontent.com/130111715/231058801-c6356f9f-c7a0-4b31-96b9-4c3a0af97977.png)

(Example)


Upon entering your password, you will be connected to a computer in the CSE basement!



________________________________________________

Now let's use some basic Unix commands. Go ahead and enter these:

1) *pwd*
2) *cd*
3) *ls*
4) *ls -a*
5) *ls -lat*
6) *mkdir*
7) *cp*

*ls* and its variations will list all the files and folders in your current directory. *pwd* will print your current directory, and *cd* can be used with a path to change your current directory. *mkdir*, short for *"make directory"* allows us to create new directories, by default in the current working directory. Here's an example of what entering some of these commands can look like:

![image](https://user-images.githubusercontent.com/130111715/231058621-061db195-d4be-4247-8ed2-71301f7267fd.png)

![image](https://user-images.githubusercontent.com/130111715/231058659-e6d33d29-8c07-4187-86e3-152cc916d997.png)
