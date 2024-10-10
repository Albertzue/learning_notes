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

Another particularly useful special shell variable is $?, which receives the exit status of the last command executed. Typically, a value of zero means that the command exited successfully, and anything other than zero indicates an error of some kind. For a complete list of special shell variables, refer to the bash man page

Reading in parameters
---
```
#!/bin/bash
read -p "Type in an adjective, noun and verb (past tense): " adj1 noun1 verb1
echo "He sighed and $verb1 to the elixir. Then he ate the $adj1 $noun1."
```

```
${var:-value}: If variable is unset or empty, expand this to value.
${var#pattern}: Chop the shortest match for pattern from the front of var's value.
${var##pattern}: Chop the longest match for pattern from the front of var's value.
${var%pattern}: Chop the shortest match for pattern from the end of var's value.
${var%%pattern}: Chop the longest match for pattern from the end of var's value.
```
```
$ THIS="Example"
$ THIS=${THIS:-"Not Set"}
$ THAT=${THAT:-"Not Set"}
$ echo $THIS
Example
$ echo $THAT
Not Set
```

Performing arithmetic in shell scripts
---
Integer arithmetic can be performed using the built-in let command or through the external expr or bc commands. After setting the variable BIGNUM value to 1024, the three commands that follow would all store the value 64 in the RESULT variable. The bc command is a calculator application that is available in most Linux distributions. The last command gets a random number between 0 and 10 and echoes the results back to you.

BIGNUM=1024
let RESULT=$BIGNUM/16
RESULT=`expr $BIGNUM / 16`
RESULT=`echo "$BIGNUM / 16" | bc`
let foo=$RANDOM; echo $foo


Another way to grow a variable incrementally is to use $(()) notation with ++I added to increment the value of I. Try typing the following:
```
$ I=0
$ echo "The value of I after increment is $((++I))"
The value of I after increment is 1
 
$ echo "The value of I before and after increment is $((I++)) and $I"
The value of I before and after increment is 1 and 2
```

Using programming constructs in shell scripts
---
```
VARIABLE=1
if [ $VARIABLE -eq 1 ] ; then
echo "The variable is 1"
fi
```

Instead of using -eq, you can use the equal sign (=), as shown in the following example. The = works best for comparing string values, while -eq is often better for comparing numbers. Using the else statement, different words can be echoed if the criterion of the if statement isn't met ($STRING = ″Friday″). **Keep in mind that it's good practice to put strings in double quotes.**
```
STRING="Friday"
if [ $STRING = "Friday" ] ; then
echo "WhooHoo. Friday."
else
echo "Will Friday ever get here?"
fi
```

you can type **help test** on the command line to get the same information like following:

| Operator |	What Is Being Tested? |
| -------- | --------------------- |
|-a file |	Does the file exist? (same as -e)|
|-b file	|Is the file a block special device?|
|-c file	|Is the file character special (for example, a character device)? Used to identify serial lines and terminal devices.|
|-d file|	Is the file a directory?|
|-e file|	Does the file exist? (same as -a)|
|-f file|	Does the file exist, and is it a regular file (for example, not a directory, socket, pipe, link, or device file)?|
|-g file	|Does the file have the set group id (SGID) bit set?|
|-h file|	Is the file a symbolic link? (same as -L)|
|-k file|	Does the file have the sticky bit set?|
