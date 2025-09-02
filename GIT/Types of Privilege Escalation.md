
2025-05-29 13:24

Status:

Tags:

# Types of Privilege Escalation

## 🔐 **Types of Privilege Escalation**

Privilege escalation refers to **gaining higher access or permissions** than originally assigned. There are two main types:

---

### 1️⃣ **Vertical Privilege Escalation**

|**Feature**|**Explanation**|
|---|---|
|📌 **Definition**|Gaining access to **higher-level privileges**, like moving from a normal user to **root/admin**.|
|🎯 **Goal**|To gain **more powerful control** over the system.|
|🛠️ **Example**|Exploiting a SUID file or vulnerable service to become **root**.|
|🔍 **Detection**|Look for unauthorized access to files, root-owned binaries, or `sudo` misconfigurations.|
|⚠️ **Risk**|High — can lead to full system compromise.|

#### ✅ Example Scenario:

- User `john` (UID 1001) runs a vulnerable program with root permissions and becomes **root** (UID 0).
    

---

### 2️⃣ **Horizontal Privilege Escalation**

|**Feature**|**Explanation**|
|---|---|
|📌 **Definition**|Gaining access to **another user’s level**, without going higher in privilege.|
|🎯 **Goal**|To **access another user's data or sessions**.|
|🛠️ **Example**|Exploiting a poorly configured application to view another user’s email or files.|
|🔍 **Detection**|Look for access to other users' home directories or sessions.|
|⚠️ **Risk**|Moderate — data exposure but not full system control.|

#### ✅ Example Scenario:

- User `alice` accesses `bob`'s private files without admin/root privileges.
    

---

### 🧠 **Summary Table**

| **Type**       | **Goal**            | **Access Level Gained**    | **Example**                  |
| -------------- | ------------------- | -------------------------- | ---------------------------- |
| **Vertical**   | Become root/admin   | Higher than current user   | Exploiting a SUID binary     |
| **Horizontal** | Act as another user | Same level, different user | Reading another user's files |


## 🔐 **Mapping Escalation Methods to Vertical & Horizontal**

|**Method**|**Type of Escalation**|**Explanation**|
|---|---|---|
|**1. Kernel Vulnerability**|✅ Vertical|Exploiting a vulnerable kernel to gain **root access** from a normal user.|
|**2. Software Vulnerability**|✅ Vertical / ✅ Horizontal|Depends on the software: you might gain **root access** or **another user's data**.|
|**3. World Writable Files**|✅ Vertical|Modify files/scripts run by **root** to execute malicious code.|
|**4. Cron Jobs**|✅ Vertical|If cron jobs are executed by **root**, injecting code escalates privileges.|
|**5. SUID**|✅ Vertical|Abuse SUID root binaries to execute commands as **root**.|
|**6. SUDO**|✅ Vertical|If misconfigured, lets users run commands as **root** without a password.|

---

## 🧠 **Special Note on Horizontal Escalation**

|**Method**|**Horizontal Use Case (if applicable)**|
|---|---|
|**Software Vulnerability**|Access another user’s data (e.g., session hijacking in a web app)|
|**World Writable Files**|Modify files owned by another **non-root user**|
|**Improper File Permissions**|View or edit files in `/home/otheruser/` or `/var/mail/username`|

---

## ✅ **Summary Table**

|**Method**|Vertical Escalation|Horizontal Escalation|Notes|
|---|---|---|---|
|Kernel Vulnerability|✅ Yes|❌ No|Direct root access|
|Software Vulnerability|✅ Yes|✅ Yes|Depends on what the software does and who runs it|
|World Writable Files|✅ Yes|✅ Sometimes|Modify root-owned or user-owned scripts|
|Cron Jobs|✅ Yes|❌ No|Only escalates if the cron job runs as root|
|SUID Binaries|✅ Yes|❌ No|Only matters if the SUID binary belongs to root|
|SUDO Misconfiguration|✅ Yes|❌ No|Run root commands if NOPASSWD or unrestricted binaries exist|


### References
