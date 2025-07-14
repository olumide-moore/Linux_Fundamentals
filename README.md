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

`cat /etc/os-release` info on running machine

`cat /proc/cpuinfo` for swap space. 

The boot process has multiple steps starting with the BIOS which triggers the boot loader to start up the Linux kernel. From there the init RAM FS file system is invoked which triggers the init program to complete the startup process and determining the appropriate distribution to deploy requires that you match your specific system needs to the capabilities of the different distributions.




#### Command Line Operations
- cat: used to type out a file (or combine files)
- head: used to show the first few lines of a file
- tail: used to show the last few lines of a file
- man : used to view documentations
- [command] --help : to get help on a command
- | (pipe): used to have the right program take the left as input e.g. `man head | head` gives the head of the head manual, `ls | wc -1`, `ls | grep *.txt`, `free -m | grep Mem`
- whoami: prints logged in user
- use `\` to seperate line of one command

Mostly inputs in the command line have three basic elements: the command, -options and arguments (e.g. `ls -a /home`)

- sudo:  allows users to run programs using the security privileges of another user (generally the superuser - root).
When running on Ubuntu and some other distributions, sudo  is already set up. If not, you can set up sudo
- Setting up sudo: 
    - run `su` in the command line and type in password to setup sudo.
    - Create a configuration file to enable your user account to use sudo- 
        `echo "[USERNAME] ALL=(ALL) ALL > /etc/sudoers.d/USERNAME`
    - If unable to modify the file, change file permission, `chmod 440 /etc/sudoers.d/[USERNAME]` 

- sudo -i : to switch to root user.

- shutdown: 
```bash
shutdown -h #halt and poweroff
         -r #reboot
sudo shutdown -h 10:00 "Shutting down for scheduled maintenance"
```
`uptime` : displays the system's uptime, how long it has been running, and when it was last booted, along with the current time, number of logged-in users, and system load averages 
`free  -m` prints memory utilisation, mem is RAM, swap is physical memory.
`df -H` prints hard disk partition utilisation 
`date`
`echo` print on screen 
`/dev/null` in Linux is a null device file. Anything written to this file is discarded (you can use as output for commands you don't want to see outputs, e.g. `sudo yum install git -y > /dev/null`)

Depending on the specifics of your particular distributions policy, programs and software packages can be installed in various directories.
In general executable programs and scripts should live in the /bin or /usr/bin or /sbin or /usr/sbin directories or somewhere under /opt. they can also appear in the /usr/local/bin or /usr/local/sbin or in a directory in a user's account space such as /home/student/bin

- `which` and `whereis`:
To find where a program resides use `which` or `whereis`. e.g. `which firefox`, `whereis firefox`. `whereis` looks in a broader range of directories.
- `locate`(requires installing mlocate) searchs for a file/directory using a database. However requires you to refresh the database for any recent files in subsequent searches. This is done by `sudo updatedb`
- `find` to look for a file/directory e.g. find in current directory `find . -name test.txt`
    `find \usr -type d -name gcc` finds directory with specified name `-type f` for finding file `-iname` finds for specified name but ignores case
   `-ctime` find based on creation time. `-mtime` based on modification time. `-size` find based on size. `-newer file` finds all the files created after file
   `find . -name searchword -exec rm {} \;` executes a command on each file found using exec (this example removes all found files). The {} is a place holder that will be filled with the found files. The command must end with /; or ;
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
- `ls -t` sort by time
- `ls -lrt` list sort by time reversed order
- `ls -R` lists files and directories recursively, including subdirectories.
<link>https://www.geeksforgeeks.org/ls-command-in-linux/</link>

`tree` displays a tree view of the filesystem
`tree -d /` view directories in the filesystem

`ln file1 file2` create a  hardlink of file1 called file2
when you then print the inode number `ls -li`, you find out file2 has same inode as file1, there's one file with different names associated with it. if one of the files is deleted the other remains.

`ln -s file1 file3` creates a soft (or symbolic) link. points file2 to file1, has a different inode number, takes no extra space on filesystem except if name is too long. when file1 is no longer available, file2 becomes a dangling link.

`wc` prints no. of lines in file
`cat file.txt` print the file contents
`cat -n file.txt` print the file contents with the line numbers
`grep word file.txt`  search the given word in the file
`grep -i word file.txt`  search the given word in the file (case insensitive)
`grep -i word *`  search the given word in all files in current directory (case insensitive)
`grep -iR word *`  search the given word in all files and directories in current directory  recursively (case insensitive)
`grep -vi word *`  search lines WITHOUT the given word (case insensitive).
`sed -i 's/test/newTEST/g' test.txt` replace the words 'test' with 'newTEST'. g is used to replace globally, if omitted, it will only replace one word per line. if you want to replace all files in the directory use * instead of test.txt, or any desired pattern matching. If you omit -i, it will only print th changes on the screen, not modify the file.

`<` right command is input for left e.g. `grep word < file.txt`
`>` : store output of left command into file specified on the right. e.g. `uptime > /tmp/systeminfo.txt`
`>>`  append to existing file
`2>>` redirect error `1>>` redirect output (default so 1 not really needed) `&>>` redirect both output and error

`less` print the file content but one screen at a time
`less -N` print the file content with line numbers but one screen at a time.
while using less, use / to search for a word in the result.
`head` for first 10 lines of the content or 'head n' for first n lines.
`tail` for last 10 lines of the content or 'tail n' for last n lines.
`tail -f` for last 10 lines and the log result dynamically updates on screen.
`tac` prints file contents backwards.
`cut -d: -f1 /etc/passwd` cut is used to print selected arts of lines from file, -d is used to specify the delimeter, -f to select the fields (in this case delimter is : and column ore of all lines is gotten)
`awk` for a smart pattern scanning more advance than cut.
```sh
awk '{ sum += $1 }; END { print sum }' file
        awk -F: '{ print $1 }' /etc/passwd
```

`touch` is often used to set or update access, change and modify times of files 
by default it resets a file's timestamp to match the current time however you can also create an empty file using touch.
`touch file{1..10}.txt` creates 10 files

`touch -t`  set the date and timestamp of a file. e.g. `touch -t 201804301015 file`

`mkdir` is used to create a deck directory
`mkdir -p` create dir with inner dirs if doesn't exist
`rmdir` is used to remove an empty directory
`rm -rf` removes a directory and all containing content recursively (include -i to get prompt before deleting)
`cp file destdir` copy file to dir
`cp -r dir destdir` copy dir to dir
`mv` can rename a file or move a file/dir to another location
`history` gives an history of all previous commands
`file filename` returns the file type
`seq 1 10` generate sequence of numbers (1 to 10 in this case). e.g. `seq 1 100 | xargs -P 5 --replace sqlite3 olutest.db 'insert into movie values({},{},{});'` #insert 1 to 100 into db table


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


## Installing packages with yum (CentOS package)
- sudo yum install vim -y  (install vim editor)

## Installing packages with apt (Ubuntu Debian package)
- `sudo apt-cache search [searchpackage]: Look for all packages that contain the given string
- `sudo apt-get install [packge]: Install package along with dependencies.
- 'apt-get remove [package]: Remove package along with dependencies.
- 

## Users and Groups
- Users and groups are used to control and grant access to files, resources or programs.
- Every user will have a unique user (uid) which is stored in /etc/passwd
- There’s also an /etc/shadow file which stores passwords in encrypted form and other information like expiry of the user.
- When new users are created, they are assigned a home directory and a program that is run when they login (usually a shell)
- Users cannot read, write, or execute each other’s files without permission 

### Linux User Types Overview


| TYPE    | EXAMPLE           | USER ID (UID)     | GROUP ID (GID)   | HOME DIRECTORY      | SHELL         |
|---------|------------------|------------------|------------------|---------------------|--------------|
| ROOT    | root             | 0                | 0                | /root               | /bin/bash    |
| REGULAR | imran, vagrant   | 1000 to 60000    | 1000 to 60000    | /home/username      | /bin/bash    |
| SERVICE | ftp, ssh, apache | 1 to 999         | 1 to 999         | /var/ftp etc        | /sbin/nologin |


- **ROOT**: The superuser account with unrestricted access to all system commands and files.
- **REGULAR**: Normal user accounts for daily use, typically assigned UIDs and GIDs in the range of 1000+.
- **SERVICE**: System service accounts used to run background processes, typically have no login shell lower UIDs and GIDs.

- `cat /etc/passwd` /etc/passwd file stores information for all user accounts. It includes a list of user accounts on the system, as well as details such as user ID, group ID, home directory, and default shell
e.g. `head- 1 /etc/passwd` gives `root:x:0:0:root:/root:/bin/bash`, format- 
username:x means there's a link to a shadow file:userid:groupid:comment:homedir:loginshell

e.g. grep vagrant /etc/passwd prints `vagrant:x:1000:1000::/home/vagrant:/bin/bash`

most other printed users are system users 

- `/etc/group/` stores group information
e.g. vagrant:x:1000:    (group id often matches the user id)
    group:x:groupid:a user in the group 
- `id [user]` gives id of the specified user and group.-
- `useradd [user]` add user e.g. useradd ansible
- `groupadd devops` create a group called devops
- `usermod -aG devops ansible` add ansible user to the group devops (G indicates adding it to a secordary group, to add it as its primary group, use lowercase g)
- you can also edit the files to add a group, i.e. `vim /etc/groups` and edit group use   rs e.g. `devops:x:1004:ansible,jenkins,aws
- To allow added users be able to login, you need to set password - `passwd [user]` (same command to reset user password)
- `su - [user]` to switch to user specified
- the root user can login to all users without filling their password 
- `last`: prints users that lasts login into the system
- `who`: prints current logged in user
- `lsof -u [user]` lists all the file the user has open (requires installing `yum install lsof -y`)
- `userdel [user]` delete user (doesn't delete the user home dir)
- `userdel -r [user]` delete user with its home dir
- `groupdel [group]` delete group

## File Permissions
- `ls -l` prints the details of file permissions
e.g.
`-rwxr-xr-x. 1 root root 44664 Aug 22  2024 /bin/login`
    - `-` --> filetype
    - `rwx` --> user (1st 3)
    - `r-x` --> group (2nd 3)
    - `r-x` --> others (3rd 3)
    - `r` --> read (you can list the contents for directories) 
    - `w` --> write (you can make changes or delete the directory)
    - `x` --> execute (you can cd for directories)
    - `-` --> regular file, 
    - `d` --> directory
    - `root root` in this case root user and root group

- `chown [options] new_owner[:new_group] file(s)`  change the file owner or group. e.g. 
 ```sh
    chown -R ansible:devops /opt/devopsdir #Change owner and group of directory recursively (i.e. owner and group of all files will change)
```
    
- `chmod [options] [mode] [File_name]` change permission or mode to directories or files e.g.
```sh
    chmod u+rwx file.txt #add rwx for owner
    chmod go-w file.txt #remove write for group and others
    chmod u+rw,go+r file.txt #read and write for owner, read-only for group and other
```
        - operators: `+`: add, `-`: remove, `=` set to specified values
        - references `u`: owner, `g`: group, `o`: others, `a`: all (owner, groups, others)
   Using numeric method, permissions are calculated by adding: 4(for read), 2(for write), 1(for execute).
   e.g. `chmod 640 file.txt read+write for uer, read for group, no permission for others` 
## Sudo
Sudo gives pwoer to a normal user to execute commands which is owned by root user (e.g. install packages). If a user has full sudoers privilege, it can become a root user anytime.
To run commands that only sudo can run, if you have sudo privileges, you use `sudo` as prefix before running the command, e.g. `sudo yum install git -y`, withouth sudo it won't run.
- `/etc/sudoers` contains. This file must be editted only with `visudo` command. It only has read permissions. In visudo editor, search for root (type `/root`), include line number with (`se nu`)
- to give user sudo priviliges, `visudo`, then in line wher you have `root    ALL=(ALL)       ALL`, add another line underneath with user, e.g. `devops    ALL=(ALL)       ALL`, to avoid it asking password, add `devops    ALL=(ALL)       NOPASSWD: ALL` instead.
- If you have syntax error in the sudoers file and you get an error while running sudo command, type e and edit the file.
- The best approach of granting  a user sudo privileges is adding a user file to the `/etc/sudoers.d` directory and adding the privilege line to that file. e.g. 
```sh
cd /etc/sudoers.d/
touch devops
vim devops #to edit the file
#then you can add 
%devops ALL=(ALL) NOPASSWD: ALL # % indicate its a group not user
```

## Package Management
The major difference between CentOS and Ubuntu is the package managment. CentOS is RPM-based, Ubuntu is Debian-based OS.
`cat /etc/os-release` lets you know what OS you are running. 
- Print installed packages: For RPM-based like CentOS, `rpm -qa`,  For Debian-based, dpkg -l.
Example installing telnet
- Find the architecture of your command, `arch` or `uname -m`
- From rpmfind.net/linux, find the telnet that matches your architecture, copy it' link address.
- Run ` curl https://rpmfind.net/linux/centos-stream/9-stream/AppStream/x86_64/os/Packages/telnet-0.17-85.el9.x86_64.rpm -o telnet-0.17-85.el9.x86_64.rpm` (`curl` is like a text-based browser, `-o` to specify the output file where it is stored)
- `rpm -ivh telnet-0.17-85.el9.x86_64.rpm` (`i` install `v` verbose (print on screen) `h` print in human readable format)
- `telnet` to verify and `quit` after. or run `rpm -qa | grep telnet`
- `rpm -e telnet-0.17-85.el9.x86_64` to uninstall (erase) package

The above is more basic way of managing packages, Linux gives much more better package management tools (yum, dnf, apt). RPM runs into issue if package requires dependencies.
e.g.
- `wget https://rpmfind.net/linux/centos-stream/9-stream/AppStream/x86_64/os/Packages/httpd-2.4.62-1.el9.x86_64.rpm` & `rpm -ivh httpd-2.4.62-1.el9.x86_64.rpm`
- `wget` or `curl` can access a remote URL, `wget` is mostly used to download from a remote URL, `curl` has many other use cases.
- `cat /etc/yum.repos.d/centos.repo` contains repositories that comes with the OS, and you can add.
- `yum search [package]` searches package from all available repositories e.g. `yum search httpd`.
-  `yum install httpd` installs the package with its dependencies.
- `dnf install httpd` dnf is the modern successor to yum. dnf has better dependency resolution, it's faster, allows for modules, allows you to undo and redo entire installations and uninstallations, and it automatically removes unused dependencies.
- `dnf remove htppd` removes the package with dependencies (that is useed by other packages).
- `dnf search  [package]`
- `dnf install epel-release -y` gives you access to more repositories. run `dnf repolist` to see the updated repos.
- If a package isn't found in your repository, you can search the package online and the vendor will give you info on how to install for your specific OS,e.g. search how to install jenkins.

## Services
You can manage services running on Linux, for instance httpd (a web service). To start a service is to start its processes, these processes can be seen when you check the service status.
- `systemctl status httpd` to see the status of the service 
- `systemctl start httpd` to start the service
- `systemctl stop httpd` to stop the service
- `systemctl restart httpd` to restart the service, maybe after making some changes.
- `systemctl reload httpd` to reload the configurations without restarting the service.
By default a service becomes inactive after reboot, unless you enable it
```sh
systemctl enable httpd
exit
sudo reboot #to reboot your server
systemctl status httpd # then after loggin in, check status and it should be active
```
- `systemctl enable --now httpd` start and enable at once
There's a service called sshd, if this service stops, you will be unable to ssh into your server. It's enabled by default. You can check its status `systemctl status sshd` 
- `systemctl is-active httpd` to directly check if it's active
- `systemctl is-enabled httpd` to directly check if it's enabled
The way systemctl works is based on a configuration file that got created when you install the service, different services configuration file is stored in `ls /etc/systemd/system/multi-user.target.wants/` e.g. running `cat /etc/systemd/system/multi-user.target.wants/httpd.service`, you will see arguments like ExecStart which specifies what binry file to run when you run `systemctl start`.

## Processes
- `top` shows you all the dynamic processes based on their consumption of CPU and RAM (similar to task manager)
- `ps aux` is similar to `top` but displays info and quits.
- `ps -ef` will not show the utilization but extra information like parent ID.
- `kill` you can kill a process similar to `systemctl stop`, killing a process will kill all its dependent process. 
e.g.
```sh
ps -ef | grep httpd | grep -v 'grep' #shows httpd processes excluding the grep process
#from the above you can note the process id of the main process which others are dependent on and kill it
kill [pid]

```
- `kill -9 [pid]` will forcefully kill a process, but will not kill its child processes (making it orphan process). (ideally, orphan processes will get cleared automatically by the system)

- `ps -ef | grep httpd | grep -v 'grep' | awk '{print $2}' | xargs kill -9`  filter to kill the process and its dependencies.

Zombie processes (aka defunct or dead processes) are processes that have completed their execution, but their entries are not removed from the process table. You can see them when you run `top`, they will have a status of Z. The best way to clear them is to reboot the system.
Orphan process is a child process that remains running even after its process is terminated.

## Archive

- `tar -czvf file.tar.gz file.txt` archive a file (c create, z compress, v verbose, f file) (`file text.tar.gz` reveals what type of file it is)
- `tar -xzvf file.tar.gz` extract files from archive
- `tar -xzvf file.tar.gz -C /opt/` extract files from archive to specified directory
Much more simpler archiving approach is zip command. 
- `yum install zim unzip -y` install the package
- `zip -r folder.zip folder` zip a folder recursively
- `unzip folder.zip` unzip

## Ubuntu commands (that differs from CentOS)
- `adduser` in ubuntu instead of `useradd` it is best to use `adduser` as `useradd` will not create an home directory for the user automatically. other user related commands in centos are fine in ubuntu.
- text editor - in ubuntu the default file editor when you run `visudo` is nano editor, to change this to vim you have run `export EDITOR=vim`, but then logging in again, you have to redo this.
The major difference between ubuntu and centos is the package management. 
e.g. to install tree package in ubuntu
```sh
#search for tree debian package for ubuntu the web and the binary package
wget http://archive.ubuntu.com/ubuntu/pool/universe/t/tree/tree_1.8.0-1_amd64.deb
dpkg -i tree_1.8.0-1_amd64.deb
```

- `dpkg -l` list all the debian packages on the machine.
- `dpkg -r tree` remove the package
- `cat /etc/apt/sources.list` lists repositories information, and you can add a repository
- `apt update` must be run before making any changes, installation or update. It checks the repositories for any package and creates a list, (yum doesn't need this as it always updates and creates and refreshes a list every 24 hours)
- `apt search tree` search for online for package
- `apt install tree` install the package (older version is `apt-get`)
- `apt install apache2` apache2 is the ubuntu equivalence of centos httpd, and it caontains dependencies. apache is a service and in ubuntu, if you install a package, is starts it automatically.
- `apt upgrade` - this actually upgrade the packages unlike `apt update` which only updates the list.
- `apt remove apache2` - removes the package.
- `apt purge apache2` - removes the package and all its configurations and data.


## Networking

**Linux and Windows networking commands** for troubleshooting and connectivity checks.  

---

## Basic Network Info

- `ifconfig` or `ip addr show` – Display network interfaces and their IP addresses (Use `/etc/hosts` to manually map hostnames to IP addresses e.g. adding `[IP address] [hostname]` to `/etc/hosts` will allow  you to `ping [hostname]`
- `ping <ip/hostname>` – Check network connectivity via ICMP packets
- `tracert <domain>` (Windows) or `traceroute <domain>` (Linux) – Show the complete path used to reach the target server ( allows you to monitor the latency of all the routes accessed to the server)
- `mtr <host>` – similar to tracert but Live view of route and packet loss between hosts (also shows live view of packets loss)

---

## Port & Service Diagnostics

- `netstat -antp` – Show open TCP ports and associated processes (run as root user to see PIDs) `ps -ef | grep <PID/name>` – Get process details using PID or name. Run `netstat -antp | grep <PID>` to get the port number used
- `ss -tunlp` – View listening ports and socket information
- `nmap <host>` – Scan for open ports on a remote machine e.g. `nmap localhost` (use carefully as it is illegal in some countries). Avoid using `nmap` on public domains without permission – may be illegal
  *(install with `apt install nmap` if needed)* 
- `telnet <ip> <port>` – Test connectivity to a specific IP and port

---

## DNS & Routing

- `dig <domain>` – Perform a DNS lookup and get record details
- `nslookup <domain>` – Similar to `dig`; older version for DNS queries
- `route -n` or `route` – Show system routing table and gateway settings
- `arp -a` – View and manage the ARP table (arp table maps IP addresses to MAC addresses, system file stored in `/proc/net/arp`) 

---

---

These commands help verify connectivity, identify network issues, and ensure services are listening on the correct ports.  
For deeper analysis, explore tools like `tcpdump` or `Wireshark`.
