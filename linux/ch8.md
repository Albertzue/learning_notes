Understanding System Administration
---
If you are the system administrator of a Linux system, you generally log in as a regular user account and then ask for administrative privileges when you need them. This is often done with one of the following:
```
su command:  Often, su is used to open a shell as root user. After the shell is open, the administrator can run multiple commands and then exit to return to a shell as a regular user.

sudo command:  With sudo, a regular user is given root privileges, but only when that user runs the sudo command to run another command.
 After running that one command with sudo, the user is immediately returned to a shell and acts as the regular user again.
Ubuntu and Fedora by default assign sudo privilege to the first user account when those systems are installed.
 This is not done by default in RHEL, although during RHEL installation, you can choose for your first user to have sudo privilege if you'd like.
```

Gaining administrative access with sudo
---
With the sudoers facility, giving full or limited root privileges to any user simply entails adding the user to /etc/sudoers and defining what privilege you want that user to have.
Then the user can run any command they are privileged to use by preceding that command with the sudo command.
```
If you look at the sudoers file in Ubuntu, you see that the initial user on the system already has privilege, by default, for the sudo group members. 
To give any other user the same privilege, you could simply add the additional user to the admin group when you run visudo.
```

To allow joe to have that privilege without using a password, type the following line instead:
```
  joe     ALL=(ALL)      NOPASSWD: ALL
```

Administrative commands
---
For the latest Ubuntu, RHEL and Fedora releases, all administrative commands from the two directories are stored in the /usr/sbin directory 
(which is symbolically linked from /sbin). Also, only /usr/sbin is added to the PATH of the root user, as well as the PATH of all regular users.

To find commands intended primarily for the system administrator, check out the section 8 manual pages (usually in /usr/share/man/man8).
They contain descriptions and options for most Linux administrative commands. If you want to add commands to your system, consider adding them to directories such as /usr/local/bin or /usr/local/sbin.
Some Linux distributions automatically add those directories to your PATH, usually before your standard bin and sbin directories.


Administrative configuration files
---

While some configuration files use standard structures, such as XML for storing information, many do not. So, you need to learn the specific structure rules for each configuration file. A comma or a quote in the wrong place can sometimes cause an entire interface to fail. You can check in many ways that the structure of many configuration files is correct.


1. /etc/default: Contains files that set default values for various utilities. For example, the file for the useradd command defines the default group number, home directory, password expiration date, shell, and skeleton directory (/etc/skel) used when creating a new user account.
2. /etc/httpd: Contains a variety of files used to configure the behavior of your Apache web server (specifically, the httpd daemon process). (On Ubuntu and other Linux systems, /etc/apache or /etc/apache2 is used instead.)
3. /etc/mail: Contains files used to configure your sendmail mail transport agent.
4. /etc/postfix: Contains configuration files for the postfix mail transport agent.
5. /etc/security: Contains files that set a variety of default security conditions for your computer, basically defining how authentication is done. These files are part of the pam (pluggable authentication modules) package.
6. /etc/skel: Any files contained in this directory are automatically copied to a user's home directory when that user is added to the system. By default, most of these files are dot (.) files, such as .kde (a directory for setting KDE desktop defaults) and .bashrc (for setting default values used with the bash shell).
7. /etc/sysconfig: Contains important system configuration files that are created and maintained by various services (including firewalld, samba, and most networking services). These files are critical for Linux distributions, such as Fedora and RHEL, that use GUI administration tools but are not used on other Linux systems at all.
8. /etc/systemd: Contains files associated with the systemd facility, for managing the boot process and system services. In particular, when you run systemctl commands to enable and disable services, files that make that happen are stored in subdirectories of the /etc/systemd system directory.


**The following are some interesting configuration files in /etc:** 

**aliases:** Can contain distribution lists used by the Linux mail services. (This file is located in /etc/mail in Ubuntu when you install the sendmail package.) 

**bashrc:** Sets system-wide defaults for bash shell users. (This may be called bash.bashrc on some Linux distributions.)
crontab: Sets times for running automated tasks and variables associated with the cron facility (such as the SHELL and PATH associated with cron).

**exports:** Contains a list of local directories that are available to be shared by remote computers using the Network File System (NFS).

**fstab:** Identifies the devices for common storage media (hard disk, DVD, CD-ROM, and so on) and locations where they are mounted in the Linux system. This is used by the mount command to choose which filesystems to mount when the system first boots.

**group:** Identifies group names and group IDs (GIDs) that are defined on the system. Group permissions in Linux are defined by the second of three sets of rwx (read, write, execute) bits associated with each file and directory.

**gshadow:** Contains shadow passwords for groups.

**host.conf:** Used by older applications to set the locations in which domain names (for example, redhat.com) are searched for on TCP/IP networks (such as the Internet). By default, the local hosts file is searched and then any name server entries in resolv.conf.

**hostname:** Contains the hostname for the local system (beginning in RHEL 7 and recent Fedora and Ubuntu systems).

**hosts:** Contains IP addresses and hostnames that you can reach from your computer. (Usually this file is used just to store names of computers on your LAN or small private network.)


**mtab:** Contains a list of filesystems that are currently mounted.

**named.conf:** Contains DNS settings if you are running your own DNS server (bind or bind9 package).

**ntp.conf:** Includes information needed to run the Network Time Protocol (NTP).

**passwd:** Stores account information for all valid users on the local system. Also includes other information, such as the home directory and default shell. (Rarely includes the user passwords themselves, which are typically stored in the /etc/shadow file.)

**profile:** Sets system-wide environment and startup programs for all users. This file is read when the user logs in.

**protocols:** Sets protocol numbers and names for a variety of Internet services.

**rpc:** Defines remote procedure call names and numbers.

**services:** Defines TCP/IP and UDP service names and their port assignments.

**shadow:** Contains encrypted passwords for users who are defined in the passwd file. (This is viewed as a more secure way to store passwords than the original encrypted password in the passwd file. The passwd file needs to be publicly readable, whereas the shadow file can be unreadable by all but the root user.)

**shells:** Lists the shell command-line interpreters (bash, sh, csh, and so on) that are available on the system as well as their locations.

**sudoers:** Sets commands that can be run by users, who may not otherwise have permission to run the command, using the sudo command. In particular, this file is used to provide selected users with root permission.
