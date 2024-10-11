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
