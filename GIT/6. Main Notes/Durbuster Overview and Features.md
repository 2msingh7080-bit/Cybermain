2024-12-20 17:11

Status:

Tags:

# Durbuster Overview and Features

**1. Purpose of Durbuster**

- **Tool Description**: Durbuster is a Java-based application designed to brute force directories and file names on web applications.
- **Functionality**:
    - Supports pure brute force attacks.
    - Allows custom wordlists to locate hidden files and directories.

---

## **Durbuster Main Window Configuration**

1. **Target URL**
    
    - Specifies the web application to test.
    - No need to mention the port if it’s the default HTTP port **80**.
2. **HTTP Method**
    
    - Options:
        - Use **GET** requests.
        - Switch between **HEAD** and **GET** methods.
3. **Multi-threading**
    
    - Durbuster allows setting the number of threads.
    - **Go Faster** option increases performance for local tests.
4. **Type of Scan**
    
    - **Pure Brute Force**:
        - Tries all possible combinations of characters.
        - Customizable parameters:
            - **Charset** (character set).
            - **Minimum and maximum word length**.
    - **List-based Brute Force**:
        - Uses preloaded wordlists.
        - Wordlist selection:
            - Example: `directory-list-2.3-small.txt` from the tool’s folder.
5. **Standard Options**
    
    - **Start Directory**: Root (`/`) by default.
    - **File Extensions**:
        - Search for specific extensions like `.bak` (backup files) and `.old` (old files).
    - **Recursive Search**:
        - Continuously scans directories for deeper files and folders.

---

## **Advanced Options**

1. **HTML Parsing Options**
2. **Authentication Options**
3. **HTTP Options**
4. **Scan Options**:
    - Limit the number of requests per second (to control traffic).
5. **Durbuster Options**

---

## **Running the Scan**

- **Launching the Tool**:
    
    - Click **Start** to begin scanning.
    - The **Results Window** provides real-time status updates.
- **Key Features in Results**:
    
    - Displays the **status** (e.g., HTTP 200 means a file exists and is accessible).
    - Allows sorting results by **file type**.

---

## **Results and Insights**

1. **Example Files Found**:
    
    - `user.bak`: Contains a list of users.
    - `CONF.old`: Includes database connection details.
2. **File Inspection**:
    
    - Right-click on files → Select **View Response** to analyze content.
3. **Tree View**:
    
    - Provides a structured view of files and directories discovered.

---

## **Saving the Scan Results**

- Go to **Report** → **Save Results**.
- Export in various formats.
- Select the desired path and generate the report.

---

## **Key Takeaways**

- Durbuster is an efficient tool for locating hidden files and directories using brute force methods.
- It provides flexibility with:
    - HTTP methods.
    - Threading and advanced options.
    - Wordlist-based or pure brute-force scanning.
- The results can reveal critical files such as user lists, backup files, and database configurations.






### References
