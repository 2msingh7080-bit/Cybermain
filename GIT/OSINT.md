2025-04-29 20:48

Status:

Tags:

# OSINT

# 26/04/25
#### Task to do 
- make report on testphp.vulnweb.com
- using maltego 
  
- Steps for making report using maltego 
	1. install maltego 
	2. make sure you login using online  verification
	3. select  and drag domain 
	4. insert IP of domain 
	5. run transfers 
	6. save it as html or pdf 

- [ ] make cheat sheet for recon-ng 
### recon-ng 

- before running recon-ng install requirements
	- marketplace install all
- first search for  modules and then use
	- modules search brute
- To load module 
	- modules load recon/domains-hosts/brute_hosts
- To view the options use 
	- options list 
- To load source / domain use 
- options set SOURCE ``<domain name >``
	- run 
- TO view the hidden ip address use  module 
	- modules search resolve
		- recon/hosts-hosts/resolve
	- run 
- To make report use module 
- module load reporting/html
- give all options 
	- options list
		- options set CUSTOMER ``<name of customer >``
		- options set CREATOR  ``<nmae>``
		- options set FILENAME ``<filenmae and path > ``
- run 


- recon-ng
marketplace install all
modules search
modules load MODULENAME
options list
options set OPTIONNAME OPTIONVALUE
options set SOURCE wipro.com
run
show hosts
show domains
to save in file use module 
reporting/csv
options set OPTIONNAME OPTIONVALUE

options set SOURCE http://testphp.vulnweb.com/
maltego
   modules load  recon/companies-multi/whois_miner

learn all section for OSINT



### References
