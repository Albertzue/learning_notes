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
