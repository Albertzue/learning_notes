**Using locate to find files by name**

On most Linux systems (Fedora and RHEL included), the updatedb command runs once per day to gather the names of files throughout your Linux system into a database. By running the locate command, you can search that database to find the location of files stored in it.

Here are a few things that you should know about searching for files using the locate command:\

There are advantages and disadvantages to using locate to find filenames instead of the find command. A locate command finds files faster because it searches a database instead of having to search the whole filesystem live. A disadvantage is that the locate command cannot find any files added to the system since the previous time the database was updated.
Not every file in your filesystem is stored in the database. The contents of the /etc/updatedb.conf file limit which filenames are collected by pruning out select mount types, filesystem types, file types, and mount points. For example, filenames are not gathered from remotely mounted filesystems (cifs, nfs, and so on) or locally mounted CDs or DVDs (iso9660). Paths containing temporary files (/tmp) and spool files (/var/spool/cups) are also pruned. You can add items to prune (or remove some items that you don't want pruned) the locate database to your needs. In RHEL 8, the updatedb.conf file contains the following:
```
PRUNE_BIND_MOUNTS = "yes"
PRUNEFS = "9p afs anon_inodefs auto autofs bdev binfmt_misc cgroup cifs coda configfs cpuset debugfs devpts ecryptfs exofs fuse fuse.sshfs fusectl gfs gfs2 gpfs hugetlbfs inotifyfs iso9660 jffs2 lustre mqueue ncpfs nfs nfs4 nfsd pipefs proc ramfs rootfs rpc_pipefs securityfs selinuxfs sfs sockfs sysfs tmpfs ubifs udf usbfs ceph fuse.ceph"
PRUNENAMES = ".git .hg .svn .bzr .arch-ids {arch} CVS"
PRUNEPATHS = "/afs /media /mnt /net /sfs /tmp /udev /var/cache/ccache /var/lib/yum/yumdb /var/lib/dnf/yumdb /var/spool/cups /var/spool/squid /var/tmp /var/lib/ceph"
```
 As a regular user, you can't see any files from the locate database that you can't see in the filesystem normally. For example, if you can't type ls to view files in the /root directory, you can't locate files stored in that directory.

When you search for a string, the string can appear anywhere in a file's path. For example, if you search for passwd, you could turn up /etc/passwd, /usr/bin/passwd, /home/chris/passwd/pwdfiles.txt, and many other files with passwd in the path.
If you add files to your system after updatedb runs, you can't locate those files until updatedb runs again (probably that night). To get the database to contain all files up to the current moment, you can simply run updatedb from the shell as root.
```
$ locate dir_color
/usr/share/man/man5/dir_colors.5.gz
…
$ locate -i dir_color
/etc/DIR_COLORS
/etc/DIR_COLORS.256color
/etc/DIR_COLORS.lightbgcolor
/usr/share/man/man5/dir_colors.5.gz
```

**Searching for files with find**
```
$ find
$ find /etc
# find /etc
$ find $HOME -ls
```
A special option to the find command is -ls. A long listing (ownership, permission, size, and so on) is printed with each file when you add -ls to the find command (similar to output of the ls -l command)

```
# find /etc -name passwd
/etc/pam.d/passwd
/etc/passwd
# find /etc -iname '*passwd*'
/etc/pam.d/passwd
/etc/passwd-
/etc/passwd.OLD
/etc/passwd
/etc/MYPASSWD
/etc/security/opasswd
```

```
$ find /usr/share/ -size +10M
$ find /mostlybig -size -1M
$ find /bigdata -size +500M -size -5G -exec du -sh {} \;
4.1G /bigdata/images/rhel6.img
606M /bigdata/Fedora-16-i686-Live-Desktop.iso
560M /bigdata/dance2.avi
```

You can search for a particular owner (-user) or group (-group) when you try to find files. By using -not and -or, you can refine your search for files associated with specific users and groups, as you can see in the following examples:
```
$ find /home -user chris -ls
131077 4 -rw-r--r--    1 chris chris  379 Jun 29 2014 ./.bashrc
# find /home \( -user chris -or -user joe \) -ls
131077 4 -rw-r--r--    1 chris chris  379 Jun 29 2014 ./.bashrc
181022 4 -rw-r--r--    1 joe   joe     379 Jun 15 2014 ./.bashrc
# find /etc -group ntp -ls
131438 4 drwxrwsr-x    3 root ntp 4096 Mar 9 22:16 /etc/ntp
# find /var/spool -not -user root -ls
262100 0 -rw-rw----    1 rpc   mail    0 Jan 27 2014 /var/spool/mail/rpc
278504 0 -rw-rw----    1 joe   mail    0 Apr  3 2014 /var/spool/mail/joe
261230 0 -rw-rw----    1 bill  mail    0 Dec 18 14:17 /var/spool/mail/bill
277373 2848 -rw-rw---- 1 chris mail 8284 Mar 15 2014 /var/spool/mail/chris
```

**Finding files by permission**
With a hyphen (-) in front of the number, all three of the bits indicated must match; with a forward slash (/) in front of it, any of the numbers can match for the search to find a file. The full, exact numbers must match if neither a hyphen nor a forward slash is used.

Consider the following examples:
```
$ find /usr/bin -perm 755 -ls
788884 28 -rwxr-xr-x   1 root       root      28176 Mar 10 2014 /bin/echo
 
$ find /home/chris/ -perm -222 -type d -ls
144503 4 drwxrwxrwx 8 chris chris 4096 Jun 23 2014 /home/chris/OPENDIR
```


**Finding files by date and time**
You just changed the contents of a configuration file, and you can't remember which one. So, you search /etc to see what has changed in the past 10 minutes:
```
 $ find /etc/ -mmin -10
```
You suspect that someone hacked your system three days ago. So, you search the system to see if any commands have had their ownership or permissions changed in the past three days:
 ```
 $ find /bin /usr/bin /sbin /usr/sbin -ctime -3
```
You want to find files in your FTP server (/var/ftp) and web server (/var/www) that have not been accessed in more than 300 days so that you can see if any need to be deleted:
 ```
 $ find /var/ftp /var/www -atime +300
```
**Finding files and executing commands**
```
 $ find /etc -iname passwd -exec echo "I found {}" \;
 I found /etc/pam.d/passwd
 I found /etc/passwd
```
```
$ grep desktop /etc/services
desktop-dna    2763/tcp              # Desktop DNA
desktop-dna    2763/udp              # Desktop DNA
 
$ grep -i desktop /etc/services
sco-dtmgr      617/tcp               # SCO Desktop Administration Server
sco-dtmgr      617/udp               # SCO Desktop Administration Server
airsync        2175/tcp              # Microsoft Desktop AirSync Protocol
…
```
In the first example, a grep for the word desktop in the /etc/services file turned up two lines. Searching again, using the -i to be case-insensitive (as in the second example), there were 29 lines of text produced.

To search for lines that don't contain a selected text string, use the -v option. In the following example, all lines from the /etc/services file are displayed except those containing the text tcp (case-insensitive):

```
$ grep -vi tcp /etc/services
```
To do recursive searches, use the -r option and a directory as an argument. The following example includes the -l option, which just lists files that include the search text, without showing the actual lines of text. That search turns up files that contain the text peerdns (case-insensitive).
```
$ grep -rli peerdns /usr/share/doc/
/usr/share/doc/dnsmasq-2.66/setup.html
/usr/share/doc/initscripts-9.49.17/sysconfig.txt
…
```

