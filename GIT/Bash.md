2025-08-27 21:29

Status:

Tags:

# Bash
- to check which bash your running 
	- ``echo $SHELL `` for linux 
	- ``which bash``

### basic script 
- for pwd
	- create shell file as 
		- ``nano ps.sh``
```bash
pwd 
echo pwd  
```
- to run make file executable
	- ``chmod +x filenmae.sh  ``
- to run file 
	- ``./ps.sh ``

- proper way to make or know is bash script or file 
	- rule 1. to write bash file 
```bash
#!/bin/bash 
```

### variables 
- variables declaration
```bash
mynmae="jay" 
```
- to print or call variable 
	- syntax 
		- ``echo $_variable_name ``
```bash
echo $_variable_name
echo $myname
```
- so to check what happens when we call  
```bash
ls="may"
echo ls 
#it gives output as ls command not as may becasue we did not use $ so 
```
- variable  .sh 

```bash
myanme="jay"
myage="25"
echo "my name is $myname."
echo "I am $myage years old."
# output
# my name is jay.
# I am 25 years old.
```
- so why do we use variables 
	- it helps in doing repetition and easy to change value with variable 

```bash
echo "linux is fun"
echo "playing games is fun"
# where as if we use variables 
word="fun"
echo "linux  is $word"
echo "playing games is $word"
```
- creating subshell using variables 
		 or 
	- printing output of command as variables
	- using ``( )``
```bash
 file =$(pwd)
 echo $file 
 #output
 # pwd 
```
- printing output of command as variables
```bash
now=$(date)
myname="jay"
echo "my name is $myname"
echo "system time and date is :$now"
echo "user name is  $USER " 
```
- to check environment variable 
	- use command 
		- ``env ``

### side points 
- when we use terminal as  to perform bash 
	- it stays for current session only 
	- and when we open or new terminal it resets 
- rules for using `` " and '``
	- in bash ``" "`` is used to  print variable value,  not variable  
	- where as ``' '`` is used to print variable, not variable value   
### References
#### shortcut keys for nano 
- ctrl + s = save
- ctrl + x = exit 
- ctrl + k = delete line  