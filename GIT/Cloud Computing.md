2025-08-23 19:25

Status:

Tags:

# Cloud Computing

### Identifying Target Cloud Environment
-  Search for HTTPS services 
	- port:443 
-  Search for AWS services
	- ssl.cert.issuer.cn:Amazon
-  Search for cloud region cloud.region:
	- <Region_code>
	- This narrows the search results to a specific geographic region within the infrastructure of the cloud provider.
- Search for Microsoft devices and services 
	- org:Microsoft
	- Obtains information about devices and services belonging to Microsoft that can be useful for identifying Azure-hosted infrastructure.
-  Search for Kubernetes
	- product:Kubernetes 
	- Obtains information on instances of Kubernetes.
-  Search for AWS services 
	- org:Amazon
	- Obtains information on services hosted specifically on Amazon’s infrastructure, which also reveals AWS-hosted services.
- Search for Azure-hosted services 
	- ssl.cert.subject.cn:azure
	- Obtains information on SSL certificates that mention Azure in the subject’s common name, indicating Azure-hosted services.
-  Search for any cloud asset
	- ``tag:cloud``
	- Obtains information on any assets tagged as being part of a cloud infrastructure. Note: The "tag" filter is only available to enterprise users.
-  Search within a specific IP range
	- net:52.0.0.0/8
	 - searches within a specific IP range, such as those assigned to AWS, where 52.0.0.0/8 is a common range for AWS.
-  Search within the instances
	- http.html:"s3.amazonaws.com"
	- Searches for instances where the HTML content mentions "s3.amazonaws.com", which could indicate the AWS S3 buckets used.
- Search for AWS-hosted services and infrastructure used by Facebook 
	- Amazon web services Facebook
	- Searches for various AWS-hosted services and infrastructure used by Facebook such as IP addresses, open ports, and service banners. This includes details on publicly accessible S3 buckets, EC2 instances, and other AWS resources associated with Facebook.
### Discovering Open Ports and Services Using Masscan
- command to run 
- ``sudo masscan -p0-65535 <target_IP_address> --rate=<rate>'``
	-  -p0-65535: Scans all ports from 0 to 65535. 
	- <target_IP_address>: Replace with the target IP address. 
	- --rate=`<rate>`: Sets the rate of packets per second. ``
- to save output file as  xml and json file `-oX` or `-oJ` 
### Vulnerability Scanning Using Prowler
- to run prowler and specify the provider 
	- ``prowler <provider>
- , Prowler generates CSV, JSON-OCSF, JSON-ASFF, and HTML reports by specifying`` -M or --output-modes`` options:
	- ``prowler <provider> -M csv json-asff json-ocsf html``
 


# Lab 1: Perform Reconnaissance on Azure
## Task 1: Azure Reconnaissance with AADInternals
- open windows 11 
1. cd  to **E:\CEH-Tools\CEHv13 Module 19 Cloud Computing\GitHub Tools\** and copy **AADInternals** folder and paste it on **Desktop**.
2. open  powershell as admonitory  
	- ``cd C:\Users\Admin\Desktop\AADInternals``
	- ``Install-Module AADInternals``
	- ``Import-Module AADInternals``
3. we will gather the publicly available information of a target Azure AD such as Tenant brand, Tenant name, Tenant ID along with the names of the verified domains.
	- ``Invoke-AADIntReconAsOutsider -DomainName company.com | Format-table`` # ec
	- council 
4.   Now, we will perform user enumeration in Azure AD, in the PowerShell window type
	- ``Invoke-AADIntUserEnumerationAsOutsider -UserName user@company.com ``
	-   We can also perform the user enumeration by placing the usernames in a text file, by running . Where the users.txt file contains the target email addresses.
		- ``Get-Content .\users.txt | Invoke-AADIntUserEnumerationAsOutsider -Method Normal``
5. To get login information for a domain
	- ``Get-AADIntLoginInformation -Domain company.com``
6.  To get the tenant ID for the given user, domain, or Access Token
	- ``Get-AADIntTenantID -Domain company.com``
7.   To get registered domains from the tenant of the given domain
	- ``Get-AADIntTenantDomains -Domain company.com``
8. Alternatively you can visit ``https://aadinternals.com/osint/`` site and type the tenant ID, domain name, or email to get the openly available information for the given tenant.

# Lab 2: Exploit S3 Buckets
## Task 1: Exploit Open S3 Buckets using AWS CLI
- you must have AWS Account 

- open parrot 
1. open terminal as sudo ``cd ~``
	-  to install AWS CLI.
		- ``pip3 install awscli``
2. To configure AWS CLI
	- ``aws configure ``

3.   
    It will ask for the following details:
    
    - AWS Access Key ID
    - AWS Secret Access Key
    - Default region name
    - Default output format
4. To provide these details, you need to login to your AWS account.
    
5. Click **Firefox** icon from the top-section of the **Desktop**.
    
6. Login to your AWS account that you created at the beginning of this task. Click the **Firefox** browser icon in the menu, type **https://console.aws.amazon.com** in the address bar, and press **Enter**.
    
    > If you do not have an AWS account, create one with the Basic Free Plan, and then proceed with the tasks.
    
7. The **Amazon Web Services Sign-In** page appears; type your email account in the **Root user email address** field and click **Next**.
    
    ![10.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/10.jpg)
    
8. Type your AWS account password in the **Password** field and click **Sign in**.
    
    > If a **Security check** window appears, enter the captcha and click on **Submit**.
    
    ![11.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/11.jpg)
    
9. Click the AWS account drop-down menu and click **Security credentials**, as shown in the screenshot.
    
    ![qw.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/qw.jpg)
    
10. Scroll down to **Access Keys** section.
    
11. Click the **Create Access Key** button. In **Continue to create access key?**; check the check box and click **Create access key**.
    
    ![qswdfghj.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/qswdfghj.jpg)
    
    ![14.2.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/14.2.jpg)
    
12. Copy the **Access Key** and switch to the **Terminal** window.
    
    ![wsdfg.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/wsdfg.jpg)
    
13. In the terminal window, right-click your mouse; select **Paste** from the context menu to paste the copied **AWS Access Key ID** and press **Enter**. It will prompt you to the **AWS Secret Access Key**. Switch to your AWS Account in the browser.
    
14. Copy the **Secret Access Key** and minimize the browser window. Switch to the **Terminal** window.
    
15. In the terminal window, right-click your mouse, select **Paste** from the context menu to paste the copied **Secret Access Key** and press **Enter**. It will prompt you for the default region name.
    
16. In the **Default region name** field, type **eu-west-1** and press **Enter**.
    
17. The **Default output format** prompt appears; leave it as default and press **Enter**.
    
    ![wsdc.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/wsdc.jpg)
    
18. For demonstration purposes, we have created an open S3 bucket with the name **certifiedhacker02** in the AWS service. We are going to use that bucket in this task.
    
    > The public S3 buckets can be found during the enumeration phase.
    
19. Let us list the directories in the certifiedhacker02 bucket. In the terminal window, type **aws s3 ls s3://[Bucket Name]** (here, Bucket Name is **certifiedhacker02**) and press **Enter**.
    
    > The bucket name may be different in your lab environment depending on the bucket you are targeting.
    
20. This will show you the list of directories in the **certifiedhacker02** S3 bucket, as shown in the screenshot.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/x2wdiqr4.jpg)
    
21. Now, maximize the browser window, type **certifiedhacker02.s3.amazonaws.com** in the address bar, and press **Enter**.
    
22. This will show you the complete list of directories and files available in this bucket.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/dk2s5snn.jpg)
    
23. Minimize the browser window and switch to **Terminal**.
    
24. Let us move some files to the certifiedhacker02 bucket. To do this, in the terminal window, type **echo "You have been hacked" >> Hack.txt** and press **Enter**.
    
25. By issuing this command, you are creating a file named **Hack.txt**.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/t3y1yxnf.jpg)
    
26. Let us try to move the **Hack.txt** file to the **certifiedhacker02** bucket. In the terminal window, type **aws s3 mv Hack.txt s3://certifiedhacker02** and press **Enter**.
    
27. You have successfully moved the **Hack.txt** file to the **certifiedhacker02** bucket.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/zdee2x5e.jpg)
    
28. To verify whether the file is moved, switch to the browser window and maximize it. Reload the page.
    
29. You can observe that the **Hack.txt** file is moved to the certifiedhacker02 bucket, as shown in the screenshot.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/wksto0td.jpg)
    
30. Minimize the browser window and switch to the **Terminal** window.
    
31. Let us delete the **Hack.txt** file from the **certifiedhacker02** bucket. In the terminal window, type **aws s3 rm s3://certifiedhacker02/Hack.txt** and press **Enter**.
    
32. By issuing this command, you have successfully deleted the **Hack.txt** file from the **certifiedhacker02** bucket.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/farjxdrj.jpg)
    
33. To verify whether the file is deleted, switch to the browser window and reload the page.
    
34. The **Hack.txt** file is deleted from the **certifiedhacker02** bucket.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/iephikvl.jpg)
    
35. Thus, you can add or delete files from open S3 buckets.
    
36. This concludes the demonstration of exploiting public S3 buckets.
    
37. Do not end the lab as we will be continuing it in next #Task.
    

**Question 19.2.1.1**

Use the AWS CLI tool to exploit open S3 buckets (certifiedhacker02) in the AWS service. Determine the command to list the total number of files available in the "certifiedhacker02" S3 bucket. Note: You must create an AWS account (https://aws.amazon.com) to perform this task. Enter the command that was used in this lab to list the contents of certifiedhacker02 bucket.






# Lab 3: Perform Privilege Escalation to Gain Higher Privileges
## Task 1: Escalate IAM User Privileges by Exploiting Misconfigured User Policy
1.   
    In the **Parrot Security** machine, click the **MATE Terminal** icon in the menu to launch the terminal.
    
2. A **Parrot Terminal** window appears. In the terminal window, type **sudo su** and press **Enter** to run the programs as a root user and user **toor** as password.
    
3. After configuring the AWS CLI, we create a user policy and attach it to the target IAM user account to escalate the privileges.
    
4. In the terminal window, type **vim user-policy.json** and press **Enter**.
    
    > This command will create a file named **user-policy** in the **attacker** directory.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/mcnyoddl.jpg)
    
5. A command line text editor appears; press **I** and type the script given below:
    
    {
    
    TypeCopy
    
    `"Version":"2012-10-17",  "Statement": [          "Effect":"Allow",          "Action":"*",          "Resource":"*"      }  ]`
    
    }
    
    > This is an AdministratorAccess policy that gives administrator access to the target IAM user.
    
    > Ignore the $ symbols in the script.
    
6. After entering the script given in the previous step, press the **Esc** button. Then, type **:wq!** and press **Enter** to save the text document.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/g30f4sd2.jpg)
    
7. Now, we will attach the created policy (**user-policy**) to the target IAM user's account. To do so, type **aws iam create-policy --policy-name user-policy --policy-document file://user-policy.json** and press **Enter**.
    
    > If you receive an error that policy already exists, rename the file and try again.
    
8. The created user policy is displayed, showing various details such as **PolicyName**, **PolicyId**, and **Arn**.
    
    ![qwdaasd.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/qwdaasd.jpg)
    
9. In the terminal, type **aws iam attach-user-policy --user-name [Target Username] --policy-arn arn:aws:iam::[Account ID]:policy/user-policy** and press **Enter**.
    
10. The above command will attach the policy (**user-policy**) to the target IAM user account (here, **test**).
    
    ![myubgfd.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/myubgfd.jpg)
    
11. Now, type **aws iam list-attached-user-policies --user-name [Target Username]** and press **Enter** to view the attached policies of the target user (here, **test**).
    
12. The result appears, displaying the attached policy name (**user-policy**), as shown in the screenshot.
    
    ![sdvsvds.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/sdvsvds.jpg)
    
13. Now that you have successfully escalated the privileges of the target IAM user account, you can list all the IAM users in the AWS environment. To do so, type **aws iam list-users** and press **Enter**.
    
14. The result appears, displaying the list of IAM users, as shown in the screenshot.
    
    ![qwdqwdqwd.jpg](https://labondemand.blob.core.windows.net/content/lab168813/instructions255490/qwdqwdqwd.jpg)
    
15. Similarly, you can use various commands to obtain complete information about the AWS environment such as the list of S3 buckets, user policies, role policies, and group policies, as well as to create a new user.
    
    - List of S3 buckets: **aws s3api list-buckets --query "Buckets[].Name"**
        
    - User Policies: **aws iam list-user-policies**
        
    - Role Policies: **aws iam list-role-policies**
        
    - Group policies: **aws iam list-group-policies**
        
    - Create user: **aws iam create-user**
        
16. This concludes the demonstration of escalating IAM user privileges by exploiting a misconfigured user policy.
    
17. Close all open windows and document all acquired information.
    

**Question 19.3.1.1**

Escalate IAM user privileges by exploiting a misconfigured user policy. Which aws command will list all user policies?

# Lab 4: Perform Vulnerability Assessment on Docker Images
## Task 1: Vulnerability Assessment on Docker Images using Trivy
1.   
    In the **Parrot Security** machine, click the **MATE Terminal** icon in the menu to launch the terminal.
    
2. A **Parrot Terminal** window appears. In the terminal window, type **sudo su** and press **Enter** to run the programs as a root user.
    
3. In the **[sudo] password for attacker** field, type **toor** as a password and press **Enter**.
    
    > The password that you type will not be visible.
    
    > Minimise the terminal for better view of output
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/ahwxj1g3.jpg)
    
4. In this lab we will be scanning two docker images, first the secure one and second the vulnerable one.
    
5. Execute command **docker pull ubuntu** to install the first docker image.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/jhm0ys0z.jpg)
    
6. Once the image is pulled we will be performing vulnerability assessment. Execute command **trivy image ubuntu**.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/lgt1vp2f.jpg)
    
7. In the above screenshot, we can observe that we have total **0** vulnerability and it's completely secure.
    
8. Now, we will analyse the vulnerbale image. execute command **docker pull nginx:1.19.6** to pull the vulnerable image.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/z5gtst4n.jpg)
    
9. Execute command **trivy image nginx:1.19.6** to scan the image.
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/s1v30p0s.jpg)
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/l50drtfi.jpg)
    
    ![Screenshot](https://labondemand.blob.core.windows.net/content/lab168813/screens/czlsp03i.jpg)
    
10. In the above screenshot we can see that we have total **401** vulnerabilities which is categorized as well along with **CVEs** mentioned.
    
11. This concludes the demonstration of vulnerability assessment on docker images using Trivy
    
12. Close all open windows and document all acquired information.
    

**Question 19.4.1.1**

In Parrot machine install ubuntu and nginx:1.19.6 images and scan with trivy security scanner. Enter the severity level that can be observed for bsdutils vulnerability of nginx:1.19.6 docker image.


- open parrot 
1. open terminal as sudo  
	- `` ``

### References
