## Linux distributions
A Linux distribution (aka distro), is a packaged version of Linux that comes with the Linux kernel plus a collection of software and utilities that make the OS functional and user-friendly. 

Each distribution packages the necessary tools to perform specialized functions, ensuring users have an optimized experience without requiring extensive setup.

There are hundrends of Linux distributions
The 3 major distributions are 
- Red Hat Family Systems: Fedora, CentOS, Oracle Linux. 
    Fedora serves as an upstream testing platform. CentOS is a close clone of RHEL. It uses yum package manager. It is widely used by enterprises who own their own systems.

- SUSE Family Systems. SLES, openSUES. SLES is upstream for openSUSE. It uses RPM0based zypper package manager for installing, updates and remove applications. It includes YaST for system admin purposes. It is widely used in retail and many other sectors. 

- Debian Family Systems. Ubuntu, Linux Mint. It is a pure open-source community project not owned by any cooperation. It focuses on stability. Ubuntu aims to provide a good compromise between long term stability and ease of use. The Debian distribution is upstream for several other dist including Ubuntu. Ubuntu in turn is upstream for Linux Mint and a number of other distributions. It's commonly used on both servers and desktop computers. It uses the DPKG-based APT package manaager. Widely used for cloud deployments. GNOME-based but differs visually. 





## Linux common terms

- Kernel is the brain of Linux system. It controls the hardware and makes it interact with the applications. Linux kernels can be found at the archive https://kernel.org/

- distribution (distro families.) is a collection of programs combined with the Linux kernel to make up a linux-based operating system. Examples of a distribution are Red Hat Enterprices Linux, Fedora, Ubuntu and Gentoo. 

- A boot loader is a program that boots the operating system. examples of boot loader are GRUB and ISOLINUX.

- A service is a program that runs as a background process. Examples are httpd, nfsd, ntpd, ftpd and named.

- A filesystem is a method for storing and organizing files in Linux. Examples include ext3, ext4, FAT, XFS, NTFS and Btrfs.

- The X Window System provides the standard toolkit and protocol to build graphical user interfaces on nearly all Linux systems.

- The Desktop Environment is a graphical user interface on top of the operating system. examples GNOME, KDE, Xfce and Fluxbox. 

- The command line is an interface for typing commands on top of the operating system.The shell is the command line interpreter that interprets the command line input and instructs the operating system to perform any necessary tasks and commands. example bash, tcsh and zsh. 

Partitions and filesystem
A partition is a physical contiguous secton of a disk or what appears to be so in some advance setup. It is a logical part of the disk. By diving the hard disk into partitions, data can be grouped and separated as needed. When a failure or mistake occurs, only the data in the affected partition will be damaged while data other partitions will likely survive. 
A filesystem is a method of storing or finding files on a hard disk using a partition.
Linux system stores its files using a layout called the Filesystem Hierarchy Standard (FHS)

![FHS](https://github.com/user-attachments/assets/19e04b09-2312-4630-9b07-8a73fa5391a5)


- `df -Th /` (df - disk free) Displays available and total disk space on the file system
- `du` used to analyze and report disk usage within directories and files (e.g. du -sh prints disk usage in a summarized human-readable format).

- Swap space: The primary function of swap space is to substitute disk space for RAM memory when real RAM fills up and more space is needed. Visit https://opensource.com/article/18/9/swap-space-linux-systems for more details on swap space. 
`cat /proc/swaps` for swap space. 



The boot process has multiple steps starting with the BIOS which triggers the boot loader to start up the Linux kernel. From there the init RAM FS file system is invoked which triggers the init program to complete the startup process and determining the appropriate distribution to deploy requires that you match your specific system needs to the capabilities of the different distributions.




#### Command Line Operations
- cat: used to type out a file (or combine files)
- head: used to show the first few lines of a file
- tail: used to show the last few lines of a file
- man : used to view documentations
- | (pipe): used to have the right program take the left as input e.g. `man head | head` gives the head of the head manual

Mostly inputs in the command line have three basic elements: the command, -options and arguments (e.g. `ls -a /home`)

- sudo:  allows users to run programs using the security privileges of another user, generally root the super user on.

- shutdown: 
```bash
shutdown -h #halt and poweroff
         -r #reboot
sudo shutdown -h 10:00 "Shutting down for scheduled maintenance"
```

Depending on the specifics of your particular distributions policy, programs and software packages can be installed in various directories.
In general executable programs and scripts should live in the /bin or /usr/bin or /sbin or /usr/sbin directories or somewhere under /opt. they can also appear in the /usr/local/bin or /usr/local/sbin or in a directory in a user's account space such as /home/student/bin

- `which` and `whereis`:
To find where a program resides use `which` or `whereis`. e.g. `which firefox`, `whereis firefox`. `whereis` looks in a broader range of directories.

- `locate` searchs for a file/directory using a dataabase. However requires you to refresh the database for any recent files in subsequent searches. This is done by `sudo updatedb`
- `find` to look for a file/directory e.g. find in current directory `find . -name test.txt`
    `find \usr -type d -name gcc` finds directory with specified name `-type f` for finding file `-iname` finds for specified name but ignores case
    - `-ctime` find based on creation time. `-mtime` based on modification time. `-size` find based on size. `-newer file` finds all the files created after file
-  `find . -name chartosearch -exec rm {} \;` executes a command on each file found using exec (this example removes all found files). The {} is a place holder that will be filled with the found files. The command must end with /; or ;
- `echo $HOME` to check your home directory.
- `pwd` displays the present working directory
- `cd ~` or `cd` to change to home directory
- `cd ..` change to parent directory
- `cd -` change to previous directory
- `cd /` change to the root directory

To keep track of traversed directories use `pushd` instead of `cd` and then `popd` will take you back in reverse order
- `dirs` lists the currently remembered directories.

- `ls` list contents in the present working directory
- `ls -a` list all files, including hidden files and directories
- `ls -l` display detailed information about the files and directories
- `ls -R` lists files and directories recursively, including subdirectories.
<link>https://www.geeksforgeeks.org/ls-command-in-linux/</link>

`tree` displays a tree view of the filesystem
`tree -d /` view directories in the filesystem

`wc` prints no of lines in file
`cat` print the file contents
`cat -n` print the file contents with the line numbers
`less` print the file content but one screen at a time
`less -N` print the file content with line numbers but one screen at a time
`head` for first 10 lines of the content or 'head -n' for first n lines.
`tail` for last 10 lines of the content or 'tail -n' for last n lines.
`tac` prints file contents backwards.
`touch` is often used to set or update access, change and modify times of files 
by default it resets a file's timestamp to match the current time however you can also create an empty file using touch.
`touch -t`  set the date and timestamp of a file. e.g. `touch -t 201804301015 file`
`mkdir` is used to create a deck directory
`rmdir` is used to remove an empty directory
`rm -rf` removes a directory and all containing content recursively (include -i to get prompt before deleting)
`mv` can rename a file or move a file to another location

#### Customizing command prompt

The $PS1 (prompt string 1) variable in Linux is an environment variable that defines the format of the command prompt displayed in the terminal.
By customizing the value of $PS1, you can personalize the appearance of your command prompt to include information such as the current username, hostname, working directory, time, and more.

Here are some common escape sequences that can be used in $PS1:

- \u: Inserts the username of the current user.
- \h: Inserts the hostname of the system.
- \w: Inserts the current working directory.
- \W: Inserts the base name of the current working directory.
- \n: Inserts a newline.
- \t: Inserts the current time in 24-hour format (HH:MM:SS).
- \d: Inserts the current date in the format "Weekday Month Day" (e.g., "Mon Sep 20").
- \$:: Inserts a $ symbol for a regular user or # symbol for the root user.

e.g. reset PS1 `PS1="\u@\h \$ "`