**Path Traversal Vulnerability - Challenge Write-Up**

### Introduction

Welcome to the **Path Traversal Vulnerability** challenge! In this task, you will be exploring a classic Path Traversal vulnerability in a web application. Your objective is to find and exploit the vulnerability to access restricted files on the server and capture the hidden flag. Path Traversal attacks allow attackers to manipulate file paths in order to access files outside the intended web directory, potentially leading to exposure of sensitive data.

In this lab, the web application fails to properly validate user input, making it vulnerable to file inclusion attacks.

### Challenge Setup

You are presented with a basic web application that includes a file access or download feature. This feature does not properly sanitize user-provided file paths, resulting in a Path Traversal vulnerability. Your goal is to find this vulnerability, craft a malicious path to access a sensitive file, and retrieve the hidden flag.

### Objective

Identify and exploit the Path Traversal vulnerability in the file access feature of the web application. Use a crafted file path to access a sensitive file outside the web root directory. Retrieve the hidden flag by exploiting this vulnerability.

### Step-by-Step Solution

#### 1. Inspect the Web Application

Open the web application’s homepage and navigate to the file access or download feature (often found on pages like `download.php` or `file.php`). This feature allows users to provide a file name or path. Enter a file name and observe how the application handles the request. Check if the input is reflected directly in the file path without proper validation.

#### 2. Craft a Path Traversal Payload

The key to solving this challenge is to manipulate the file path and move up the directory structure to access a sensitive file, such as `/etc/passwd` on a Linux system or `C:\Windows\System32\drivers\etc\hosts` on a Windows system. Try injecting a basic path traversal payload like:

```plaintext
../../etc/passwd
```

Submit the form with this payload. If successful, you will see the contents of the `passwd` file or another sensitive file being displayed.

#### 3. Capture the Flag

Now that you’ve confirmed the presence of a Path Traversal vulnerability, the next step is to retrieve the hidden flag. The flag is typically stored in a system file, often in a specific directory such as `/var/www/flag.txt`. Use the following payload to access the flag:

```plaintext
../../var/www/flag.txt
```

Submit this payload to retrieve the contents of the file, which will contain the flag. The flag might look like this:

```plaintext
FLAG{_*}
```

### Example Output

After successfully injecting the path traversal payload, you will see the contents of the sensitive file, including the hidden flag, like this:

```plaintext
FLAG{_*}
```

### 4. Remediation

In real-world applications, preventing Path Traversal vulnerabilities is crucial. Here are some best practices to avoid such vulnerabilities:

- **Input Validation:** Always validate and sanitize user-provided file paths. Ensure that inputs are restricted to specific directories and that special characters like `../` are blocked.
- **Use Whitelists:** Limit file access to a whitelist of acceptable files or directories, ensuring that users cannot access unintended files.
- **Absolute File Paths:** Use absolute file paths within the application to ensure that user inputs cannot manipulate relative file paths.
- **File System Permissions:** Ensure the web server has proper file system permissions to prevent access to sensitive system files.

### 5. Conclusion

This challenge highlights the risk of Path Traversal vulnerabilities in web applications. By following proper input validation, directory restrictions, and implementing strong file system permissions, developers can mitigate the risk of such vulnerabilities. Congratulations on completing the challenge!

### 6. References

- [OWASP Path Traversal Cheat Sheet](https://owasp.org/www-community/attacks/Path_Traversal)
- [Mozilla Developer Network (MDN) - Path Traversal](https://developer.mozilla.org/en-US/docs/Web/Security)
