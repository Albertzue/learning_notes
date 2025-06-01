```
$ cd ~
$ pwd
/home/chris
$ cd ~/Music
$ pwd
/home/chris/Music
$ cd ../../../usr
$ pwd
/usr
```
The tilde (~) represents your home directory. So cd ~ takes you there. You can use the tilde to refer to directories relative to your home directory as well, such as /home/chris/Music with ~/Music. Typing a name as an option takes you to a directory below the current directory, but you can use two dots (..) to go to a directory above the current directory. The example shown takes you up three directory levels (to /), and then takes you into the /usr directory


**Using Metacharacters and Operators**
```
*	Matches any number of characters.
?	Matches any one character.
[…]	Matches any one of the characters between the brackets, which can include a hyphen-separated range of letters or numbers.
```
```
$ ls ????e
apple grape
$ ls g???e*
grape grapefruit
The first example matches any five-character file that ends in e (apple, grape). The second matches any file that begins with g and has e as its fifth character (grape, grapefruit).
```
```
$ ls [abw]*
apple banana watermelon
$ ls [agw]*[ne]
apple grape watermelon
$ ls [a-g]*
apple banana grape grapefruit
```
```
<	Directs the contents of a file to the command. In most cases, this is the default action expected by the command and the use of the character is optional; using less bigfile is the same as less < bigfile.
>	Directs the standard output of a command to a file. If the file exists, the content of that file is overwritten.
2>	Directs standard error (error messages) to the file.
&>	Directs both standard output and standard error to the file.
>>	Directs the output of a command to a file, adding the output to the end of the existing file.
```

**Using brace expansion characters**
By using curly braces ({}), you can expand out a set of characters across filenames, directory names, or other arguments to which you give commands. For example, if you want to create a set of files such as memo1 through memo5, you can do that as follows:
```
$ touch memo{1,2,3,4,5}
$ ls
memo1 memo2 memo3 memo4 memo5

$ touch {John,Bill,Sally}-{Breakfast,Lunch,Dinner}
$ ls
Bill-Breakfast Bill-Lunch John-Dinner Sally-Breakfast Sally-Lunch
Bill-Dinner John-Breakfast John-Lunch Sally-Dinner
$ rm -f {John,Bill,Sally}-{Breakfast,Lunch,Dinner}
$ touch {a..f}{1..5}
$ ls
a1 a3 a5 b2 b4 c1 c3 c5 d2 d4 e1 e3 e5 f2 f4
a2 a4 b1 b3 b5 c2 c4 d1 d3 d5 e2 e4 f1 f3 f5
```

**understanding File Permissions and Ownership**
The chmod command also can be used recursively. For example, suppose that you wanted to give an entire directory structure 755 permission (rwxr-xr-x), starting at the $HOME/myapps directory. To do that, you could use the -R option, as follows:
```
$ chmod -R 755 $HOME/myapps
```


**Setting default file permission with umask**
```
$ umask 777 ; touch file01 ; mkdir dir01 ; ls -ld file01 dir01
d---------. 2 joe joe 6 Dec 19 11:03 dir01
----------. 1 joe joe 0 Dec 19 11:02 file01
$ umask 000 ; touch file02 ; mkdir dir02 ; ls -ld file02 dir02
drwxrwxrwx. 2 joe joe 6 Dec 19 11:00 dir02/
-rw-rw-rw-. 1 joe joe 0 Dec 19 10:59 file02
$ umask 022 ; touch file03 ; mkdir dir03 ; ls -ld file03 dir03
drwxr-xr-x. 2 joe joe 6 Dec 19 11:07 dir03
-rw-r--r--. 1 joe joe 0 Dec 19 11:07 file03
```
If you want to change your umask value permanently, add a umask command to the .bashrc file in your home directory (near the end of that file). The next time you open a shell, your umask is set to whatever value you chose.

**Changing file ownership**

To change both user and group to joe, you could enter the following instead:
```
# chown joe:joe /home/joe/memo.txt
# ls -l /home/joe/memo.txt
-rw-r--r--. 1 joe joe 0 Dec 19 11:23 /home/joe/memo.txt

# chown -R joe:joe /media/myusb
```
