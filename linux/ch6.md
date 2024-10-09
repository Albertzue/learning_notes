**Listing processes with ps**
```
$ ps u
USER  PID   %CPU  %MEM  VSZ  RSS  TTY  STAT  START  TIME  COMMAND
jake  2147  0.0   0.7   1836 1020 tty1 S+    14:50  0:00  -bash
jake  2310  0.0   0.7   2592 912  tty1 R+    18:22  0:00  ps u
```
the u option (equivalent to -u) asks that usernames be shown\
The STAT column represents the state of the process, with R indicating a currently running process and S representing a sleeping process.\
START shows the time the process began running, and TIME shows the cumulative system time used. (Many commands consume very little CPU time,
as reflected by 0:00 for processes that haven't even used a whole second of CPU time.)

VSZ (virtual set size) shows the size of the image process (in kilobytes), and RSS (resident set size) shows the size of the program in memory. 
The VSZ and RSS sizes may be different because VSZ is the amount of memory allocated for the process, 
whereas RSS is the amount that is actually being used. RSS memory represents physical memory that cannot be swapped.

. For example, the next example lists every running process (-e) and then follows the -o option with every column of information I want to display, including

the process ID (pid), username (user), user ID (uid), group name (group), group ID (gid), virtual memory allocated (vsz), resident memory used (rss), and the full command line that was run (comm). By default, output is sorted by process ID number.
```
$ ps -eo pid,user,uid,group,gid,vsz,rss,comm | less
  PID USER UID GROUP GID    VSZ   RSS COMMAND
  1   root 0   root    0 187660 13296 systemd
  2   root 0   root    0      0     0 kthreadd
```

If you want to sort by a specific column, you can use the sort= option. For example, to see which processes are using the most memory, I sort by the vsz field. That sorts from lowest memory use to highest. Because I want to see the highest ones first, I put a hyphen in front of that option to sort (sort=-vsz).
```
$ ps -eo pid,user,group,gid,vsz,rss,comm --sort=-vsz | head
     PID USER  GROUP  GID    VSZ   RSS COMMAND
  2366 chris chris 1000 3720060 317060 gnome-shell
  1580 gdm   gdm     42 3524304 205796 gnome-shell
  3030 chris chris 1000 2456968 248340 firefox
  3233 chris chris 1000 2314388 316252 Web Content
```

**Listing and changing processes with top**
1. Press h to see help options, and then press any key to return to the top display.
2. Press M to sort by memory usage instead of CPU, and then press P to return to sorting by CPU.
3. Press the number 1 to toggle showing CPU usage of all your CPUs if you have more than one CPU on your system.
4. Press R to reverse sort your output.
5. Press u and enter a username to display processes only for a particular user.
