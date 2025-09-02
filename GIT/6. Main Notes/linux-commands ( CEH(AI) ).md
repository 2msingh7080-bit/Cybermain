2025-03-22 00:07

Status:

Tags:  version V1 - [[GIT/linux-commands-md]]


# linux-commands (CEH)
# Linux Commands

## VirtualBox Network Settings and Initial Update
- VM Management - Snapshot, Clone, Export VM

## Terminal
One of the most common ways to interact with linux-based system is via the command-line (SHELL)
- user $
- root #

### Shell - terminal/console
- `sh` - Bourn shell (Foundation - important tasks, scripting language)
- `bash` - Bourne-Again shell
- `ksh` - Korn shell (handles loop syntax better than bash)
- `zsh` - Z shell

> [!tip] Shell Tip
> To verify current shell execute `ps $$`

## Package Management - apt, dpkg

```bash
man apt
sudo apt update
sudo apt upgrade metasploit-framework
apt-cache search <packagename>
apt install <packagename>
apt remove --purge <packagename>
apt autoremove
dpkg -i <packagename>
```

## System information
```bash
uname
hostname
hostname -I
whoami
id
ifconfig
ip addr
ip a
```

## Moving around
```bash
pwd (Absolute and Relative path)
ls
ls -larti
cd
whereis
tree
```

## File operations
```bash
touch
mkdir
cat
cat /etc/os-release
cat /etc/passwd
cat /etc/shadow
cat ~/.bash_history
nano <filename>
leafpad <filename>
mousepad <filename>
pluma <filename>
file
cp
mv
rmdir
rm -rf
```

> [!warning] Caution
> Cat when used with single redirection operator (`>`) will write or replace the existing contents of the file.

To kill process: `ctrl+c`  
To pause the process: `ctrl+z`

To append content to the existing file we must use two redirection operators (`>>`).

`mv` command is used to move one file contents to another file or to move a file into existing directory.
`mv` command is also used to rename a file or directory. To rename we need to provide file or directory name that exists followed by file or directory name that does not exist.

```bash
nano <filename>
ctrl+x
y
enter
leafpad <filename>
mousepad <filename>
pluma <filename>
```

> [!example] Practice Example
> Read the content of `/usr/share/wordlists/dirb/small.txt` and copy the first 7 lines in to file named as result.txt on users desktop.
> - What is the file size?
> - How many lines contain the letter 'a'?

## Managing Users
```bash
#Create user with home directory
adduser <username>
```

## Managing Groups
Primary group - By default linux will create a group with same username. It is recorded in `/etc/passwd`  
Secondary group - The group to which users are added. It is recorded in `/etc/group` file.

```bash
#To verify which groups the user belongs to
groups <username>
#To add new group
addgroup <groupname>
#To add a user to sudo group
usermod -aG <groupname> <username>
usermod -aG sudo <username>
usermod -rG sudo <username>
```

## File permissions
To change ownership: `chown`  
To change permissions: `chmod`

| Type | Symbol | Value |
|------|--------|-------|
| user/owner | u | - |
| group | g | - |
| others | o | - |
| read | r | 4 |
| write | w | 2 |
| execute | x | 1 |

```bash
#To change file or directory ownership
sudo chown root:kali <file/directoryname>
#To change file or directory permissions
sudo chmod o+w <file/directoryname>
sudo chmod g-r <file/directoryname>
sudo chmod +x <file/directoryname>
sudo chmod 755 <file/directoryname>
```

## Executing commands as privileged user
```bash
whoami
sudo whoami
#To verify sudo rights of a user
sudo -l
#To allow current user to run a loginshell as root user
sudo -i
#We can use su to access user account that has been disabled
sudo su
su -
```

The contents of `/etc/sudoers`

`root ALL=(ALL:ALL) ALL`

| Field | Meaning |
|-------|---------|
| First field | Username that the rule will apply to (root) |
| 1st ALL | This rule applies to all hosts |
| 2nd ALL | The root user can run commands as all users |
| 3rd ALL | The root user can run commands as all groups |
| Last ALL | The rules apply to all commands |

```bash
sudo visudo -f /etc/sudoers
%ceh ALL=ALL, /usr/bin/cat
%sudo ALL=ALL, !/bin/nmap
ben ALL=(ALL:ALL) /usr/bin/cat
kali ALL=(root) NOPASSWD: /usr/bin/cat
nik ALL=(bob) NOPASSWD: /usr/bin/nano
```

## Streams, Redirection and piping

File streams:
- standard output - stdout (1)
- standard input - stdin (0)
- standard error - stderr (2)

Output redirects: `>`, `>>`  
Input redirects: `<`  
Piping: `|`

```bash
ls -l > file1
ls /etc >> file1
cat file1 file2 file3 > file4
cat < names.txt
ls -l /root 2>error.txt
locate ls 2>error.txt
ls -1 | wc -l
ls -l /etc | more
cp
mv
rmdir
rm -rf
```

> [!note] Note
> `2>&1` - Send standard error to where ever standard output is being redirected

```bash
date
time
cal
```

## Searching files
- `locate` - uses a prebuilt database, which should be regularly updated - `sudo updatedb`
- `find` - to recursively search any given path for various files

```bash
locate <keyword/filename>
locate nc.exe
find . -name "file"
find / -name *.nse
find / -name *.conf 2>errors.txt
find / -name "*.txt" 2>/dev/null
find / ! -user kali -type f
```

## Take backups
```bash
tar -cf <backup.tar> *
tar -rf <existingarchive> <newfiletoappend>
tar -xvf backup.tar
gzip <file/dir names>
gzip -d <backup.tar.gz>
gunzip <backup.tar.gz>
zip <newfilename.zip> <filestocompress>
unzip <filename.zip>
zip -e <newfilename.zip> <filestocompress>
zip
bzip2
xz
```

| Command | Description |
|---------|-------------|
| more | view text file one page at a time |
| less | same as more with navigation |
| head | by default display first 10 lines of file |
| tail | display last 10 lines of a file |

```bash
more <filename>
more -10 <filename>
less <filename>
head -15 <filename>
tail <filename>
```

## Text processing
- `cut` - to cut parts of lines from specified file
- `grep` (global regular expression print) - searches a file for a particular pattern of characters, and displays all lines that contain that pattern.

```bash
#To display first or specific characters of every line in file
cut -c1 <filename>
cut -c1,2,4 <filename>
cut -c1-5 <filename>
cut -d : -f 1 /etc/passwd
ls -l | cut -c2-4
env | grep SHELL
ls | grep txt
lscpu | grep "model name"
lscpu | grep -i "model name"
grep "kali" /etc/passwd
grep "/bin/false" /etc/passwd
grep John contacts.txt
grep -w John contacts.txt
grep -wi John contacts.txt
grep ^J contacts.txt
grep .com$ contacts.txt
grep -win -B4 john contacts.txt
grep -win -A4 john contacts.txt
grep -e "Cartel" -e "Hacker" about.txt
grep -E "Naveen|Kumar" names.txt
egrep -i "Naveen|Kumar" names.txt
```

## Command Cheatsheet

| Command | Category | Purpose |
|---------|----------|---------|
| `ls -larti` | File Navigation | List all files with details |
| `sudo apt update` | Package Management | Update package lists |
| `cat /etc/passwd` | File Operations | View system user accounts |
| `chmod 755 file` | Permissions | Set read/write/execute permissions |
| `grep -i pattern file` | Text Processing | Case-insensitive pattern search |
| `tar -xvf backup.tar` | Backups | Extract tar archive |
| `find / -name "*.txt"` | Searching | Find all text files |
### References