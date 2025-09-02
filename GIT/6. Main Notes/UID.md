2025-05-29 13:01

Status:

Tags:

# UID

- Example :
- uid=1001
- uid=1001

|UID/GID|Purpose|Defined By|Listed in|
|---|---|---|---|
|0|`root` user|Linux|`/etc/passwd` + `nss-systemd`|
|1…4|System users|Distributions|`/etc/passwd`|
### 📌 **What is a UID?**

- UID stands for **User Identifier**.
    
- It's a **unique number** assigned to **every user** on a Linux system.
    
- The system uses UIDs (not usernames) to **track user permissions** and ownerships.
    

---

### 🧩 **Basic UID Ranges and Meaning**

|UID Range|Purpose / Type of User|
|---|---|
|**0**|**Root user** (superuser with all permissions)|
|**1–99**|**System-reserved UIDs** (for system processes or daemons)|
|**100–999**|**Reserved for system users** (created during package/software installs)|
|**1000+** (or 1001+)|**Regular users** created by admin or during OS installation|

> 📌 **Note**: On some distros like Ubuntu, normal users start from `1000`, but on others, like CentOS, it might start from `500`.

---

### 📂 **Where is UID Stored?**

- UID is stored in the `/etc/passwd` file.
    
```bash
cat /etc/passwd 
```

Example line:
```bash
john:x:1001:1001:John:/home/john:/bin/bash 
```
Breakdown:

- `john` – Username
    
- `x` – Encrypted password (placeholder)
    
- **`1001`** – UID
    
- `1001` – GID (Group ID)
    
- `John` – Full name or description
    
- `/home/john` – Home directory
    
- `/bin/bash` – Shell
    

---

### 🛡️ **Special UID - Root (UID 0)**

- The **root account** always has UID **0**
    
- Any user with UID 0 has **unrestricted access** to the entire system.
    

---

### 🔎 **Check Your UID**

Use:


```bash
id -u 
```

Or:

```bash
id username 
```


---

### ✅ **Quick Summary**

| UID     | Type of User        | Description                         |
| ------- | ------------------- | ----------------------------------- |
| 0       | Root                | Full system access                  |
| 1–99    | System Processes    | Internal system accounts            |
| 100–999 | System Applications | Services or apps (e.g., `www-data`) |
| 1000+   | Regular Users       | Human users like you and me         |

---

### 📁 Example from `/etc/passwd`

|**Username**|**UID**|**GID**|**Home Directory**|**Shell**|
|---|---|---|---|---|
|`root`|0|0|`/root`|`/bin/bash`|
|`john`|1001|1001|`/home/john`|`/bin/bash`|
|`mysql`|112|117|`/nonexistent`|`/usr/sbin/nologin`|

### References
