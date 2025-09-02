2025-02-19 17:00

Status:

Tags:

# Linux Command Line Prompts

#### **Overview**

When using the **command-line interface (CLI)** in Linux, the terminal displays a **prompt**, which indicates that the system is ready to accept user input.

---

### **1. Understanding the Command Prompt Symbols**

- The **prompt** is typically shown as a **blinking cursor** next to a **symbol** that represents the user type.
- Different symbols indicate different user roles:

|Symbol|Meaning|
|---|---|
|**$**|Normal user|
|**#**|Root (Administrator)|
|**%**|C Shell user (Tcsh, Csh)|

---

### **2. Home Directory Symbol (~)**

- The **tilde (~)** represents the **home directory** of the user.
- When you first log in, your default location is **your home directory**.

---

### **3. Variations in Prompts Across Distributions**

- Different **Unix/Linux distributions** may have slightly different prompt formats due to **default settings**.
- However, most **prompts** include key details such as:
    - **Username**
    - **Machine hostname**
    - **Current working directory**
    - **Ending symbol** ($, %, or #)

---

### **4. Example Prompts in Different Shells**

|Shell Type|Example Prompt|
|---|---|
|**Bash (Default in Linux)**|`user@hostname:~$`|
|**Root User (Administrator Mode)**|`root@hostname:~#`|
|**C Shell (Tcsh, Csh)**|`user@hostname:~%`|

---

### **Summary**

- **$** → Normal user, **#** → Root user, **%** → C Shell user.
- The **tilde (~)** represents the home directory.
- Prompts **vary across distributions** but usually display **username, hostname, and directory**.




### References
