the default shell for most Linux systems is called bash, the **Bourne Again SHell**

Executing and debugging shell scripts
---
1. The filename is used as an argument to the shell (as in bash myscript). In this method, the file does not need to be executable; it just contains a list of shell commands. The shell specified on the command line is used to interpret the commands in the script file. This is most common for quick, simple tasks.
2. The shell script may also have the name of the interpreter placed in the first line of the script preceded by #! (as in #!/bin/bash) and have the execute bit of the file containing the script set (using chmod +x filename). You can then run your script just as you would any other program in your path simply by typing the name of the script on the command line.

You can use set -x near the beginning of the script to display each command that is executed or launch your scripts using
```
 $ bash -x myscript
```

Special shell positional parameters
---
There are special variables that the shell assigns for you. One set of commonly used variables is called positional parameters or command-line arguments, 
and it is referenced as $0, $1, $2, $3…$n. $0 is special, 
and it is assigned the name used to invoke your script; the others are assigned the values of the parameters passed on the command line in the order they appeared. 
For instance, 
let's say that you had a shell script named myscript which contained the following:
```
#!/bin/bash
# Script to echo out command-line arguments
echo "The first argument is $1, the second is $2."
echo "The command itself is called $0."
echo "There are $# parameters on your command line"
echo "Here are all the arguments: $@"
```
