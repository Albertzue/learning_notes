ch3 
---
```
$ date
Thu Jun 29 08:14:53 EDT 2019
```
```
$ pwd
/home/chris
$ hostname
mydesktop
$ ls
Desktop   Downloads Pictures Templates
Documents Music     Public   Videos
```
```
$ ls --hide=Desktop
Documents Music Public Videos
Downloads Pictures Templates
```
In the previous example, the --hide option tells the ls command not to display the file or directory named Desktop when listing the contents of the directory.\
Notice that the equal sign immediately follows the option (no space) and then the argument (again, no space).
```
$ uname
Linux
$ uname -a
Linux mydesktop 5.3.7-301.fc31.x86_64 #1 SMP Mon Oct 21 19:18:58 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
```
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:↵
/home/chris/bin
```
The results show a common default path for a regular Linux user. Directories in the path list are separated by colons. Most user commands that come with Linux are stored in the /bin, /usr/bin, or /usr/local/bin directory. The /sbin and /usr/sbin directories contain administrative commands (some Linux systems don't put those directories in regular users' paths). The last directory shown is the bin directory in the user's home directory (/home/chris/bin).

Built-in command. This is a command built into the shell. As a result, there is no representation of the command in the filesystem. Some of the most common commands that you will use are shell built-in commands, such as cd (to change directories), echo (to output text to the screen), exit (to exit from a shell), fg (to bring a command running in the background to the foreground), history (to see a list of commands that were previously run), pwd (to list the present working directory), set (to set shell options), and type (to show the location of a command).


**!n** Run command number. Replace the n with the number of the command line and that line is run. For example, here's how to repeat the date command shown as command number 382 in the preceding history listing:
 ```
 $ !382
 date
 Fri Jun 29 15:47:57 EDT 2019
```
**!!—!!** Run previous command. Runs the previous command line. Here's how you would immediately run that same date command:
```
 $ !!
 date
 Fri Jun 29 15:53:27 EDT 2019
```
**!?string—?** Run command containing string. This runs the most recent command that contains a particular string of characters. For example, you can run the date command again by just searching for part of that command line as follows:
```
 $ !?dat?
 date
 Fri Jun 29 16:04:18 EDT 2019
 ```

**Expanding commands**
With command substitution, you can have the output of a command interpreted by the shell instead of by the command itself. In this way, you can have the standard output of a command become an argument for another command. The two forms of command substitution are $(command) and `command` (backticks, not single quotes).

The command in this case can include options, metacharacters, and arguments. The following is an example of using command substitution:
```
$ vi $(find /home | grep xyzzy)
```

Sometimes, you want to pass arithmetic results to a command. There are two forms that you can use to expand an arithmetic expression and pass it to the shell: $[expression] or $(expression). The following is an example:
```
$ echo "I am $[2020 - 1957] years old."
I am 63 years old.
```

**Using Shell Variables**

You can see all variables set for your current shell by typing the set command. A subset of your local variables is referred to as environment variables. Environment variables are variables that are exported to any new shells opened from the current shell. Type env to see environment variables.


**Configuring your shell**

**/etc/profile	**
```
This sets up user environment information for every user. It is executed when you first log in. This file provides values for your path in addition to setting environment variables for such things as the location of your mailbox and the size of your history files. Finally, /etc/profile gathers shell settings from configuration files in the /etc/profile.d directory.|
```
**/etc/bashrc	**
```
This executes for every user who runs the bash shell each time a bash shell is opened. It sets the default prompt and may add one or more aliases. Values in this file can be overridden by information in each user's ~/.bashrc file.|
```

**~/.bash_profile**	
```
This is used by each user to enter information that is specific to his or her use of the shell. It is executed only once—when the user logs in. By default, it sets a few environment variables and executes the user's .bashrc file. This is a good place to add environment variables because, once set, they are inherited by future shells.
```
**~/.bashrc**	
```
This contains the information that is specific to your bash shells. It is read when you log in and also each time you open a new bash shell. This is the best location to add aliases so that your shell picks them up.
```
**~/.bash_logout**
```
This executes each time you log out (exit the last bash shell).
```
