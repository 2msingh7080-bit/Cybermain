2025-02-14 19:43

Status:

Tags:

# Linux Commands

 
### Basic Commands 

| commands                   | function                                                                    | Option                                                                                                                                                                                        | Examples                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| apt                        | software installations                                                      |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt update            | updating system and checks for any update                                   |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt upgrade           | instating update or yes                                                     |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt dist -upgrade - y | upgrading new distribution version                                          |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt install           |                                                                             |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt remove            | removes application, but does not dependence file                           |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt purge             | removes dependence file                                                     |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt autoremove        | automatically removes dependence file                                       |                                                                                                                                                                                               |                                                                                                                            |
| sudo apt search            | searches for particular applucation                                         |                                                                                                                                                                                               |                                                                                                                            |
| sudp apt list              | list of software installed                                                  |                                                                                                                                                                                               |                                                                                                                            |
| sudp apt -h                |                                                                             |                                                                                                                                                                                               |                                                                                                                            |
|                            |                                                                             |                                                                                                                                                                                               |                                                                                                                            |
|                            |                                                                             |                                                                                                                                                                                               |                                                                                                                            |
| cd                         | Change directory                                                            |                                                                                                                                                                                               |                                                                                                                            |
| cd ..                      | pervious directory                                                          |                                                                                                                                                                                               |                                                                                                                            |
| cd -                       | pervious path                                                               |                                                                                                                                                                                               |                                                                                                                            |
| ls                         | List files and directories                                                  |                                                                                                                                                                                               |                                                                                                                            |
| ls -l                      | displays files and directories with detailed information                    |                                                                                                                                                                                               |                                                                                                                            |
| ls -a                      | shows all files and directories, including                                  |                                                                                                                                                                                               |                                                                                                                            |
| ls -lh                     | displays file sizes in a human-readable format.                             |                                                                                                                                                                                               |                                                                                                                            |
|                            |                                                                             |                                                                                                                                                                                               |                                                                                                                            |
| pwd                        | displays the current working directory                                      |                                                                                                                                                                                               |                                                                                                                            |
| nano                       | creating text files                                                         |                                                                                                                                                                                               |                                                                                                                            |
| touch                      | Creates files or updates access and modification times                      |                                                                                                                                                                                               |                                                                                                                            |
| chmod                      | Change file permissions                                                     | u: User/owner permissions.<br>g: Group permissions.<br>o: Other permissions.<br>- ****+****: Add permissions.<br>- ****–****: Remove permissions.<br>- ****=****: Set permissions explicitly. | chmod u+rwx file.txt<br>    <br>grants read, write, and execute permissions to the owner of the file.<br>chmod +1 filename |
| sudo -i                    | change into root user                                                       |                                                                                                                                                                                               |                                                                                                                            |
| su name                    | change from root user another user                                          |                                                                                                                                                                                               |                                                                                                                            |
| mkdir                      | Create a new directory                                                      | mkdir name                                                                                                                                                                                    | mkdir my_directo                                                                                                           |
| whoami                     | tells  current user                                                         |                                                                                                                                                                                               | whoami <br>root                                                                                                            |
| hostname                   | tells current host                                                          |                                                                                                                                                                                               | hostname <br>kali                                                                                                          |
| sudo hostname              | changes host name                                                           |                                                                                                                                                                                               | sudo hostname mayak <br>root㉿mayank                                                                                        |
| grep                       | used for searching and matching text patterns within files                  | **global regular expression print**                                                                                                                                                           | grep google                                                                                                                |
| &&                         | is used for combining tow commands                                          |                                                                                                                                                                                               | apt update && apt upgrade                                                                                                  |
| --help                     | to display their usage instructions                                         |                                                                                                                                                                                               | ls --help                                                                                                                  |
| man                        | Displays the detailed manual (man page)                                     |                                                                                                                                                                                               | man ls                                                                                                                     |
| uname                      | used to display system-related information                                  | <br>                                                                                                                                                                                          |                                                                                                                            |
| whereis                    | used to locate the binary, source,manual page files for a specified command |                                                                                                                                                                                               | whereis ls<br> /bin/ls /usr/share/man/man1/ls.1.gz                                                                         |
| history                    | list of previously executed commands                                        |                                                                                                                                                                                               |                                                                                                                            |



### Steps for installation and uninstallation 
 1. sudo apt update 
 2. sudo apt install "XXX"
 To remove software 
 1. sudo apt remove "XXX" (removes application)
 2. sudo apt purge "XXX" (removes dependence file)
 3. sudo apt autoremove (automatically removes dependence file)
---
### File creating, edit and remove 
//owner//group//permission// 
EX: -rw-rw-r-- 1 kali kali 58 Feb 14 10:46 1.text
Read ---r--4 
Write ---w---2 
Execute---x---1

creating text files 
1. nano 1.text
Giving permission for Executing 
1. chmod +1 filename
2. chmod o+wr filename 
Remove permission for Executing 
1. chmod -1 filename
2. chmod o-wr filename 

#### Command 

| Command | function                                                 | Option                                                                                                                                                                                        | Examples                                                                                                                   |
| ------- | -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| mkdir   | Create a new directory                                   | mkdir name                                                                                                                                                                                    | mkdir my_directo                                                                                                           |
| rmdir   | removes directory (if folder is empty)                   | rmdir name                                                                                                                                                                                    | rmdir mysaca                                                                                                               |
| rm -rf  | deletes files and directories forcefully                 | rm -rf name                                                                                                                                                                                   |                                                                                                                            |
| cd      | Change directory                                         |                                                                                                                                                                                               |                                                                                                                            |
| cd ..   | pervious directory                                       |                                                                                                                                                                                               |                                                                                                                            |
| ls      | List files and directories                               |                                                                                                                                                                                               |                                                                                                                            |
| ls -l   | displays files and directories with detailed information |                                                                                                                                                                                               |                                                                                                                            |
| ls -a   | shows all files and directories, including               |                                                                                                                                                                                               |                                                                                                                            |
| ls -lh  | displays file sizes in a human-readable format.          |                                                                                                                                                                                               |                                                                                                                            |
|         |                                                          |                                                                                                                                                                                               |                                                                                                                            |
| pwd     | displays the current working directory                   |                                                                                                                                                                                               |                                                                                                                            |
| nano    | creating text files                                      |                                                                                                                                                                                               |                                                                                                                            |
| touch   | Creates files or updates access and modification times   |                                                                                                                                                                                               |                                                                                                                            |
| chmod   | Change file permissions                                  | u: User/owner permissions.<br>g: Group permissions.<br>o: Other permissions.<br>- ****+****: Add permissions.<br>- ****–****: Remove permissions.<br>- ****=****: Set permissions explicitly. | chmod u+rwx file.txt<br>    <br>grants read, write, and execute permissions to the owner of the file.<br>chmod +1 filename |
### Network Commands 

| Command          | function                                                                                             | Option                      | Examples                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------- | --------------------------- | ------------------------------------------------------------- |
| ifconfig         | Display network interface information                                                                |                             |                                                               |
| netstat -ant<br> | Display network connections and statistics.                                                          |                             | netstat -tul<br> shows all listening TCP and UDP connections. |
| nslookup         |                                                                                                      |                             |                                                               |
| dig              | used for DNS lookup                                                                                  | Domain Information Groper   | dig google.com                                                |
| wget             | download files such as HTTP, HTTPS, FTP, and FTPS protocols                                          |                             | weget https://www.wipro.com/                                  |
| arp              | communication protocol that maps IP addresses to the physical MAC addresses of devices within  (LAN) | Address Resolution Protocol |                                                               |
### To check TCP connections 
netstat 
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 10.0.2.15:50254         maa03s43-in-f3.1e1:http ESTABLISHED
tcp        0      0 10.0.2.15:48418         93.243.107.34.bc.:https ESTABLISHED
tcp        0      0 10.0.2.15:45498         209.100.149.34.bc:https ESTABLISHED
tcp        0      0 10.0.2.15:58642         maa03s39-in-f2.1e:https ESTABLISHED
tcp        0      0 10.0.2.15:49848         broadband.actcorp.:http ESTABLISH


### To see route 
traceroute google.com
traceroute to google.com (142.250.205.238), 30 hops max, 60 byte packets
 1  10.0.2.2 (10.0.2.2)  0.314 ms  0.259 ms  0.214 ms
 2  * * * (this mean firewall is holding back)
 3  * * *
 4  * * *

Gives about DNS 
nslookup googl.com   
Server:         10.0.2.3
Address:        10.0.2.3#53

Non-authoritative answer:
Name:   googl.com
Address: 142.250.193.100
Name:   googl.com
Address: 2404:6800:4007:81f::2004

| Command | function                                                                                             | Option                      | Examples                     |
| ------- | ---------------------------------------------------------------------------------------------------- | --------------------------- | ---------------------------- |
| dig     | used for DNS lookup                                                                                  | Domain Information Groper   |                              |
| wget    | download files such as HTTP, HTTPS, FTP, and FTPS protocols                                          |                             | weget https://www.wipro.com/ |
| arp     | communication protocol that maps IP addresses to the physical MAC addresses of devices within  (LAN) | Address Resolution Protocol |                              |

### User commands 

| Command       | function                                                                    | Option      | Examples                                           |
| ------------- | --------------------------------------------------------------------------- | ----------- | -------------------------------------------------- |
| sudo -i       | change into root user                                                       |             |                                                    |
| su name       | change from root user another user                                          |             |                                                    |
| mkdir         | Create a new directory                                                      | mkdir name  | mkdir my_directo                                   |
| rmdir         | removes directory (if folder is empty)                                      | rmdir name  | rmdir mysaca                                       |
| rm -rf        | deletes files and directories forcefully                                    | rm -rf name |                                                    |
| whoami        | tells  current user                                                         |             | whoami <br>root                                    |
| hostname      | tells current host                                                          |             | hostname <br>kali                                  |
| sudo hostname | changes host name                                                           |             | sudo hostname mayak <br>root㉿mayank                |
| useradd       | adds new user                                                               |             | useradd eve                                        |
| passwd        | changes the password for user                                               |             | passwd kali                                        |
| userdel       | deletes the user                                                            |             | userdel eve                                        |
| groupadd      | add new group                                                               |             | groupadd itcell                                    |
| uermod -aG    | adds user to group                                                          |             | uermod -aG group name username                     |
| groupdel      | deletes the group                                                           |             | group  itcell                                      |

****make sure you learn about user file , user password file, group file and group file locartion ****


### processor

| Command | function                                             | Option | Examples   |
| ------- | ---------------------------------------------------- | ------ | ---------- |
| top     | gives information about process <br>like task manger |        |            |
| htop    | better than top                                      |        |            |
| ps -e   | gives information about process with id              |        |            |
| ps aux  |                                                      |        |            |
| kill    | terminates any thing                                 |        |            |
| kill -9 | kills forcefully                                     |        | kill -9 id |
|         |                                                      |        |            |
### compression and decompression of file  
tar is  used for creating, viewing, and extracting files from archives
- **Common Options:**
    
    - `-c`: Creates a new archive
        
    - `-x`: Extracts files from an archive
        
    - `-f`: Specifies the archive file name
        
    - `-t`: Lists the contents of an archive.
        
    - `-v`: Provides verbose output, showing files as they are processed.
        
    - `-z`: Compresses the archive using gzip, resulting in a `.tar.gz` file.
        
    - `-j`: Compresses the archive using bzip2, resulting in a `.tar.bz2` file
Example:
compress 
tar cvf file.tar 1.text

uncompress file  
tar xcf file.tar 1.text 

| Command  | function                            | Option | Examples                  |
| -------- | ----------------------------------- | ------ | ------------------------- |
| zip      | zip a file                          |        | zip may.zip 1.txt         |
| unzip    | unzip a file                        |        | unzip may.zip             |
| unzip -d | unzip a file in different directory |        | unzip may.zip -d /desktop |

| Command                   | function                                               | Option | Examples                                   |
| ------------------------- | ------------------------------------------------------ | ------ | ------------------------------------------ |
| tar cvf file.tar filename | compress file                                          |        | tar cvf file.tar 1.text                    |
| tar xcf file.tar filename |                                                        |        | tar xcf file.tar 1.text                    |
| rm                        | deletes a file                                         |        | rm 1.text                                  |
| rm -f                     | forcefuly deletes                                      |        |                                            |
| rm -r                     | deletes a directory                                    |        |                                            |
| cp                        | copy flie                                              |        |                                            |
| mv                        | rename file                                            |        |                                            |
| mv                        | move file                                              |        |                                            |
| cat                       | display file                                           |        |                                            |
| locate                    | for finding files and directories based on their names |        | locate 1.text<br>/home/kali/Desktop/1.text |
| sort -r                   | sort file content in reverse                           |        |                                            |
 **chechk 1:10:10 and learn about it **


Lynis
 
##  ew course commands
| &&         | is used for combining tow commands                                          |      | apt update && apt upgrade                          |
| ---------- | --------------------------------------------------------------------------- | ---- | -------------------------------------------------- |
| --help     | to display their usage instructions                                         |      | ls --help                                          |
| man        | Displays the detailed manual (man page)                                     |      | man ls                                             |
| uname      | used to display system-related information                                  | <br> |                                                    |
| whereis    | used to locate the binary, source,manual page files for a specified command |      | whereis ls<br> /bin/ls /usr/share/man/man1/ls.1.gz |
| history    | list of previously executed commands                                        |      |                                                    |
| history -c | clears history of commands                                                  |      |                                                    |
|            |                                                                             |      |                                                    |
|            |                                                                             |      |                                                    |
## Shortcut Keys 

Advance keys = [here](https://www.youtube.com/watch?v=sCx_J8GWa-4)
Linux Advance courses [here](https://www.youtube.com/playlist?list=PLtK75qxsQaMLZSo7KL-PmiRarU7hrpnwK)
command line [here](https://www.youtube.com/watch?v=avg65oY7sj4)

### Terminal Shortcuts

| Shortcut Keys  | Function                                                                |
| -------------- | ----------------------------------------------------------------------- |
| **Ctrl + A**   | Move cursor to the beginning of the line.                               |
| **Ctrl + E**   | Move cursor to the end of the line.                                     |
| **Ctrl + C**   | Cancel the current command.                                             |
| **Ctrl + D**   | Exit the terminal or send EOF (End-of-file) marker.                     |
| **Ctrl + L**   | Clear the terminal screen.                                              |
| **Ctrl + R**   | Search command history (backward search).                               |
| **Ctrl + U**   | Erase everything from the cursor position to the beginning of the line. |
| **Ctrl + Z**   | Suspend the current process (can be resumed with `fg`).                 |
| **Tab**        | Auto-complete commands, files, or directories.                          |
| **Up Arrow**   | Show the previous command from history.                                 |
| **Down Arrow** | Show the next command from history.                                     |

### Navigation and Window Management

| Shortcut Keys   | Function                                 |
| --------------- | ---------------------------------------- |
| **Alt + Tab**   | Switch between open windows.             |
| **Alt + F1**    | Open the applications menu.              |
| **Alt + F2**    | Open the run dialog to execute commands. |
| **Alt + F4**    | Close the current window.                |
| **Alt + F5**    | Restore window to normal size.           |
| **Alt + F7**    | Move the current window.                 |
| **Alt + F8**    | Resize the current window.               |
| **Alt + F9**    | Minimize the current window.             |
| **Alt + F10**   | Maximize the current window.             |
| **Alt + Space** | Open the window menu.                    |

### Virtual Terminals

| Shortcut Keys       | Function                                     |
| ------------------- | -------------------------------------------- |
| **Ctrl + Alt + F1** | Switch to the first virtual terminal.        |
| **Ctrl + Alt + Fn** | Switch to the nth virtual terminal (n=1..6). |

### Desktop Environment Shortcuts

| Shortcut Keys        | Function                                                |
| -------------------- | ------------------------------------------------------- |
| **Super Key**        | Opens the desktop menu (varies by desktop environment). |
| **Super + S**        | Workspace overview.                                     |
| **Ctrl + Shift + C** | Copy selected text in terminal.                         |
| **Ctrl + Shift + V** | Paste selected text in terminal.                        |

### Miscellaneous

| Shortcut Keys | Function                                              |
| ------------- | ----------------------------------------------------- |
| **PrtScn**    | Take a screenshot of the whole desktop.               |
| **Ctrl + Q**  | Quit applications (not standard in all environments). |
 
## Chat gpt table  
| **Command**  | **Description**                              |
| ------------ | -------------------------------------------- |
| `ls`         | List directory contents                      |
| `cd`         | Change directory                             |
| `pwd`        | Print working directory                      |
| `mkdir`      | Create a new directory                       |
| `rmdir`      | Remove an empty directory                    |
| `rm`         | Remove files or directories                  |
| `cp`         | Copy files and directories                   |
| `mv`         | Move/rename files                            |
| `touch`      | Create an empty file                         |
| `cat`        | Display the contents of a file               |
| `find`       | Search for files                             |
| `locate`     | Find a file quickly                          |
| `updatedb`   | Update the database for `locate`             |
| `tree`       | Display directory structure                  |
| `lsattr`     | List file attributes                         |
| `chattr`     | Change file attributes                       |
| `stat`       | Display detailed file information            |
| `df`         | Show disk usage                              |
| `du`         | Show directory size                          |
| `mount`      | Mount a filesystem                           |
| `umount`     | Unmount a filesystem                         |
| `chmod`      | Change file permissions                      |
| `chown`      | Change file owner                            |
| `chgrp`      | Change file group                            |
| `umask`      | Set default permissions                      |
| `ls -l`      | View file permissions                        |
| `ps`         | Display running processes                    |
| `top`        | Show real-time process usage                 |
| `htop`       | Interactive process monitoring               |
| `kill`       | Terminate a process by PID                   |
| `killall`    | Kill a process by name                       |
| `pkill`      | Kill a process by pattern                    |
| `jobs`       | List background jobs                         |
| `bg`         | Resume a background job                      |
| `fg`         | Bring a background job to the foreground     |
| `nice`       | Start a process with a specific priority     |
| `renice`     | Change process priority                      |
| `whoami`     | Display the current user                     |
| `who`        | Show logged-in users                         |
| `w`          | Display active users                         |
| `id`         | Show user ID and group ID                    |
| `groups`     | Show groups of a user                        |
| `passwd`     | Change user password                         |
| `su`         | Switch user                                  |
| `sudo`       | Execute commands as root                     |
| `adduser`    | Add a new user                               |
| `deluser`    | Delete a user                                |
| `usermod`    | Modify user accounts                         |
| `groupadd`   | Add a new group                              |
| `groupdel`   | Delete a group                               |
| `ping`       | Check network connectivity                   |
| `hostname`   | Display hostname                             |
| `ifconfig`   | Show IP configuration                        |
| `ip`         | Show/manipulate IP addresses                 |
| `netstat`    | Show network connections                     |
| `ss`         | Show socket statistics                       |
| `traceroute` | Trace a network route                        |
| `nslookup`   | Query DNS records                            |
| `dig`        | Get DNS information                          |
| `wget`       | Download files from a URL                    |
| `curl`       | Fetch data from a URL                        |
| `scp`        | Securely copy files between systems          |
| `sftp`       | Secure file transfer                         |
| `rsync`      | Sync files between systems                   |
| `fdisk`      | Partition a disk                             |
| `mkfs`       | Create a filesystem                          |
| `fsck`       | Check and repair a filesystem                |
| `blkid`      | Show block device UUID                       |
| `tune2fs`    | Modify filesystem parameters                 |
| `df -h`      | Show disk space usage in human-readable form |
| `du -sh`     | Show directory size                          |
| `tar`        | Archive files                                |
| `zip`        | Compress files into a ZIP archive            |
| `unzip`      | Extract a ZIP archive                        |
| `gzip`       | Compress files using Gzip                    |
| `gunzip`     | Decompress Gzip files                        |
| `bzip2`      | Compress files using Bzip2                   |
| `bunzip2`    | Decompress Bzip2 files                       |
| `xz`         | Compress files using XZ                      |
| `unxz`       | Decompress XZ files                          |
| `echo`       | Print text to the console                    |
| `cat`        | Display file contents                        |
| `tac`        | Display file contents in reverse             |
| `head`       | Display first few lines of a file            |
| `tail`       | Display last few lines of a file             |
| `less`       | View file contents one screen at a time      |
| `more`       | View file contents (older version of `less`) |
| `grep`       | Search text in files                         |
| `awk`        | Pattern scanning and text processing         |
| `sed`        | Stream editor for modifying text             |
| `cut`        | Remove sections of each line                 |
| `sort`       | Sort lines of text                           |
| `uniq`       | Remove duplicate lines                       |
| `uname -a`   | Display system information                   |
| `uptime`     | Show system uptime                           |
| `date`       | Display current date and time                |
| `cal`        | Show a calendar                              |
| `free -h`    | Show memory usage                            |
| `dmesg`      | Show system boot messages                    |
| `history`    | Show command history                         |

### References
