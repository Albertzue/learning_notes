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

Using journalctl to view the systemd journal
---
```
# journalctl
# journalctl --list-boots | head
-2 93bdb6164… Sat 2020-01-04 21:07:28 EST—Sat 2020-01-04 21:19:37 EST
-1 7336cb823… Sun 2020-01-05 10:38:27 EST—Mon 2020-01-06 09:29:09 EST
 0 eaebac25f… Sat 2020-01-18 14:11:41 EST—Sat 2020-01-18 16:03:37 EST
# journalctl -b 488e152a3e2b4f6bb86be366c55264e7
# journalctl -k
```
In these examples, the journalctl command with no options lets you page through all messages in the systemd journal. To list the boot IDs for each time the system was booted, use the –list-boots option. To view messages associated with a particular boot instance, use the -b option with one of the boot instances. To see only kernel messages, use the -k option. Here are some more examples:
```
# journalctl _SYSTEMD_UNIT=sshd.service
# journalctl PRIORITY=0
# journalctl -a -f
```
Use the _SYSTEMD_UNIT= options to show messages for specific services (here, the sshd service) or for any other systemd unit file (such as other services or mounts). To see messages associated with a particular syslog log level, set PRIORITY= to a value from 0 to 7. In this case, only emergency (0) messages are shown. To follow messages as they come in, use the -f option; to show all fields, use the -a option.

Checking your hardware
---
There are a few ways to view kernel boot messages after Linux comes up. Any user can run the dmesg command to see what hardware was detected and which drivers were loaded by the kernel at boot time. As new messages are generated by the kernel, those messages are also made available to the dmesg command.
```
NOTE
After your system is running, many kernel messages are sent to the /var/log/messages file. So, for example, if you want to see what happens when you plug in a USB drive, you can type tail -f /var/log/messages and watch as devices and mount points are created. Likewise, you could use the journalctl -f command to follow messages as they come into the systemd journal.
```

The lspci command lists PCI buses on your computer and devices connected to them. Here's a snippet of output:
```
$ lspci
00:00.0 Host bridge: Intel Corporation
     5000X Chipset Memory ControllerHub
00:02.0 PCI bridge: Intel Corporation 5000 Series Chipset
     PCI Express x4 Port 2
00:1b.0 Audio device: Intel Corporation 631xESB/632xESB
     High Definition Audio Controller (rev 09)
00:1d.0 USB controller: Intel Corporation 631xESB/632xESB/3100
     Chipset UHCI USBController#1 (rev 09)
07:00.0 VGA compatible controller: nVidia Corporation NV44
0c:02.0 Ethernet controller: Intel Corporation 82541PI
     Gigabit Ethernet Controller (rev 05)
```

f you are specifically interested in USB devices, try the lsusb command. By default, lsusb lists information about the computer's USB hubs along with any USB devices connected to the computer's USB ports:
```
$ lsusb
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 413c:2105 Dell Computer Corp.
    Model L100 Keyboard

Bus 002 Device 004: ID 413c:3012 Dell Computer Corp.
    Optical Wheel Mouse
Bus 001 Device 005: ID 090c:1000 Silicon Motion, Inc. -
    Taiwan 64MB QDI U2 DISK
```

Removing modules
---
Use the rmmod command to remove a module from a running kernel. For example, to remove the module parport_pc from the current kernel, type the following:
```
# rmmod parport_pc
```
