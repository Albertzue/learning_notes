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

```
$ jobs
[1]  Stopped (tty output) vi /tmp/myfile
[2]  Running        find /usr -print > /tmp/allusrfiles &
[3]  Running        nroff -man /usr/man2/* >/tmp/man2 &
[4]- Running        nroff -man /usr/man3/* >/tmp/man3 &
[5]+ Stopped        nroff -man /usr/man4/* >/tmp/man4
```
The plus sign (+) next to number 5 shows that it was most recently placed in the background. The minus sign (-) next to number 4 shows that it was placed in the background just before the most recent background job. Because job 1 requires terminal input, it cannot run in the background. As a result, it is Stopped until it is brought to the foreground again.


**Using foreground and background commands**
```
$ fg %1
```

If a command is stopped, you can start it running again in the background using the bg command. For example, refer back to job 5 from the jobs list in a previous example:
```
[5]+ Stopped nroff -man /usr/man4/*>/tmp/man4
```
Enter the following:
```
$ bg %5
```
After that, the job runs in the background. Its jobs entry appears as follows:
```
[5] Running nroff -man /usr/man4/*>/tmp/man4 &
```

**Killing processes with kill and killall**

Signals are represented by both numbers and names. Signals that you might send most commonly from a command include SIGKILL (9), SIGTERM (15), and SIGHUP (1). The default signal is SIGTERM, which tries to terminate a process cleanly. To kill a process immediately, you can use SIGKILL. The SIGHUP signal can, depending on the program, tell a process to reread its configuration files. SIGSTOP pauses a process, while SIGCONT continues a stopped process.


| Signal   | Number  | Description|
| -------- | ------- | ------- |
|SIGHUP	   |1	       | Hang-up detected on controlling terminal or death of controlling process.|
|SIGINT	   |2        | Interrupt from keyboard.
|SIGQUIT	 |3	       | Quit from keyboard.
|SIGABRT	 |6	       |Abort signal from abort(3).
|SIGKILL	 |9	       |Kill signal.
|SIGTERM	 |15	     |Termination signal.
|SIGCONT	 |19,18,25 |Continue if stopped.
|SIGSTOP	 |17,19,23 |Stop process.
```
$ kill 10432
$ kill -15 10432
$ kill -SIGKILL 10432
```
The default signal sent by kill is 15 (SIGTERM), so the first two examples have exactly the same results. On occasion, a SIGTERM doesn't kill a process, so you may need a SIGKILL to kill it. Instead of SIGKILL, you can use –9 to get the same result.

**Using killall to signal processes by name**

With the killall command, you can signal processes by name instead of by process ID. The advantage is that you don't have to look up the process ID of the process that you want to kill. The potential downside is that you can kill more processes than you mean to if you are not careful. (For example, typing killall bash may kill a bunch of shells that you don't mean to kill.)


**Setting processor priority with nice and renice**

1.The lower the nice value, the more access to the CPUs the process has. In other words, the nicer a process is, the less CPU attention it gets. So, a –20 nice value gets more attention than a process with a 19 nice value.
2. A regular user can set nice values only from 0 to 19. No negative values are allowed. So a regular user can't ask for a value that gives a process more attention than most processes get by default.
3. A regular user can set the nice value higher, not lower. So, for example, if a user sets the nice value on a process to 10 and then later wants to set it back to 5, that action will fail. Likewise, any attempt to set a negative value will fail.
4. A regular user can set the nice value only on the user's own processes.
5. The root user can set the nice value on any process to any valid value, up or down.
```
# nice -n +5 updatedb &
# renice -n -5 20284
```

