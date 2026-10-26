# What is Secure Coding?

## What is secure coding?

Secure coding is the practice of public, private, and cryptographically altered code for the purpose of protecting information, systems, and infrastructure from unauthorized or malicious actors who might wish to gain access to such information for the purpose of personal gain or social disruption.

## What is a reasonable scope of secure coding?

It must be relevant to the product. For example, if you are coding for financial transactions or governmental communications, you might have maximum protective and cryptographic protocols around it. If you are hardening a service from unauthorized access or unlicensed use, you might choose to use 3-5 protocols protecting against the most common modes of attack with wider protection and session windows to reduce blast radius of an attack.

## CWE/SANS Top 25

**Assignment:** List and describe in your own words, using 1-3 sentences for each of the CWE/SANS Top 25. Each one should have its own unique URL as a reference from where you got it, for example:

https://cwe.mitre.org/top25/archive/2025/2025_cwe_top25.html

### 1. Improper Neutralization of Input During Web Page Generation (“Cross-site Scripting”)

https://cwe.mitre.org/data/definitions/79.html

This seems to be addressing user inputs and making them inert so an attacker cannot place a script in a user input field that is then used to gain access to other parts of the environment.

### 2. Improper Neutralization of Special Elements used in a SQL Command (SQL Injection)

https://cwe.mitre.org/data/definitions/89.html

This is similar to the first one. It is dealing with a user input that is shaped as a SQL command which can alter the database or even allow information to be obtained that shouldn’t.

### 3. Cross-Site Request Forgery (CSRF)

https://cwe.mitre.org/data/definitions/352.html

This is something that cannot easily be done with blockchain. A bad actor uses some kind of spoof to trick the target system they have authorization to by impersonating the correct credentials. The victim system does not or cannot properly verify the user is valid and allows the action.

### 4. Missing Authorization

https://cwe.mitre.org/data/definitions/862.html

The product does not perform an authorization check to make sure the ID trying to gain access should be in the system or have the information they are accessing.

### 5. Out-of-bounds Write

https://cwe.mitre.org/data/definitions/787.html

Out-of-bounds writes are attacks on memory buffers which seek to break the system and force a retry. When they system reboots, there can be an opportunity to write to the target CPU, bypassing the safety checks. This was how the Nintendo 3DS was hacked in 2014. The game Cubic Ninja had a level creation and share feature whereby users could create their own levels and share them with friends via QR code. The level data encoded in the QR code was loaded into fixed-length buffers without any length checks. The hacker created a malformed QR code whose level data was oversized and overflowed the buffer, smashing the stack. The code execution then triggered the download and execution of a boot.3dsx launcher from the SD card, which then installed the Homebrew Channel.

### 6. Improper Limitation of a Pathname to a Restricted Directory (Path Traversal)

https://cwe.mitre.org/data/definitions/22.html

An attacker uses some kind of user input to construct a pathname that is intended to identify a file or directory that is located underneath a restricted directory.

```yaml
path_access:
  restricted_root: "/authorized/directory"
  user_input:
    requested_path: "../../unauthorized_directory/file"
  application:
    constructed_path: "/authorized/directory/../../unauthorized_directory/file"
    canonical_path: "/unauthorized_directory/file"
  validation:
    required:
      canonical_path_within_restricted_root: true
  result:
    if_validation_missing: "unauthorized_access"
    if_validation_passes: "authorized_access"
    if_validation_fails: "denied"
```

### 7. Use After Free

https://cwe.mitre.org/data/definitions/416.html

This one took me a little while to wrap my head around. It’s a pointer whose memory address has been cleared and can be re-assigned but the original pointer still points to that memory address. So if the new assigned memory matches or can be formed logically into the same form as the expected value of the first object the pointer was expecting, you can have unintended consequences, even privilege escalation.

### 8. Out-of-bounds Read

https://cwe.mitre.org/data/definitions/125.html

Basically, if you do not check for the minimum value of the expected buffer, you can start reading from memory surrounding the expected buffer.

### 9. Improper Neutralization of Special Elements Used in an OS Command (OS Command Injection)

https://cwe.mitre.org/data/definitions/78.html

An application takes user input and incorporates it into an operating system command without properly separating the data from the command syntax. This can allow an attacker to execute additional commands with the permissions of the application.

### 10. Improper Control of Generation of Code (Code Injection)

https://cwe.mitre.org/data/definitions/94.html

An application dynamically generates executable code using input that has not been properly validated. An attacker can manipulate that input to change the intended program behavior or introduce executable instructions that the developer never intended.

### 11. Buffer Copy without Checking Size of Input

https://cwe.mitre.org/data/definitions/120.html

Buffer expects a certain length but doesn’t check that the input is equal or less than the expected length and the overflow is copied into adjacent memory.

### 12. Unrestricted Upload of File with Dangerous Type

https://cwe.mitre.org/data/definitions/434.html

An application allows users to upload files without adequately checking their type, content, or intended use. An attacker could upload an executable script or another dangerous file that the server subsequently processes, potentially allowing unauthorized code execution. This is how level 6 of the xss-game is solved.

### 13. NULL Pointer Dereference

https://cwe.mitre.org/data/definitions/476.html

A program attempts to access memory through a pointer that contains a NULL value instead of a valid memory address. This can cause a crash or unexpected behavior.

### 14. Stack-based Buffer Overflow

https://cwe.mitre.org/data/definitions/121.html

A program writes more data into a stack-allocated buffer than it has room to store. The extra data can overwrite adjacent stack memory, potentially corrupting variables, control information, or return addresses, resulting in crashes or unintended code execution.

### 15. Deserialization of Untrusted Data

https://cwe.mitre.org/data/definitions/502.html

An application receives serialized data and reconstructs objects from it without adequately verifying that the data is trustworthy. An attacker can manipulate the serialized information to cause unexpected object behavior, change application state, or potentially execute malicious code, depending on the deserialization mechanism.

### 16. Heap-based Buffer Overflow

https://cwe.mitre.org/data/definitions/122.html

This is similar to a stack-based buffer overflow, except the affected memory is dynamically allocated on the heap. Writing beyond the allocated buffer can corrupt adjacent objects or memory-management structures.

### 17. Incorrect Authorization

https://cwe.mitre.org/data/definitions/863.html

The application performs an authorization check, but the check is implemented incorrectly. This can allow a user to peerform an action or access a resource beyond their intended permissions, even though an authorization mechanism technically exists.

### 18. Improper Input Validation

https://cwe.mitre.org/data/definitions/20.html

An application accepts input without adequately checking that it conforms to the expected format, type, range, or permitted values. This can allow unexpected data to enter parts of the application that were designed around assumptions the input does not satisfy.

### 19. Improper Access Control

https://cwe.mitre.org/data/definitions/284.html

The application does not properly enforce restrictions on who or what can access particular resources or perform certain operations. This is a broad category that includes failures in authentication, authorization, and the enforcement of intended access boundaries.

### 20. Exposure of Sensitive Information to an Unauthorized Actor

https://cwe.mitre.org/data/definitions/200.html

An application unintentionally exposes information to someone who should not have access to it. This could include credentials, internal system details, personal information, or confidential records disclosed through error messages, responses, logs, or other interfaces.

### 21. Missing Authentication for Critical Function

https://cwe.mitre.org/data/definitions/306.html

The application provides access to an important function without first verifying the identity of the person or system attempting to use it.

### 22. Server-Side Request Forgery (SSRF)

https://cwe.mitre.org/data/definitions/918.html

An application allows user-controlled input to influence requests made by the server to other network destinations. An attacker can potentially redirect those requests toward internal services or otherwise inaccessible resources, using the server's network access to reach systems they cannot contact directly.

### 23. Improper Neutralization of Special Elements Used in a Command (Command Injection)

https://cwe.mitre.org/data/definitions/77.html

An application constructs commands using untrusted input without properly handling characters that have special meaning to the receiving command interpreter. This can allow an attacker to modify or append instructions, and it applies more broadly than operating system commands alone.

### 24. Authorization Bypass Through User-Controlled Key

https://cwe.mitre.org/data/definitions/639.html

An application uses a user-controlled identifier or key to select a resource without properly verifying whether the requester is authorized to access it. An attacker may be able to change an identifier, such as an account number or record ID, to access another user's information.

### 25. Allocation of Resources Without Limits or Throttling

https://cwe.mitre.org/data/definitions/770.html

An application allows users or processes to consume system resources without adequate limits. An attacker can exploit this to exhaust memory, CPU time, storage, connections, or other resources, potentially degrading performance or causing a denial of service.

## Final Question

**Which one of the 25 listed are you most interested in and why?**

Stack-based buffer overflow. This was used to gain access to the Nintendo 3DS through a game called Cubic Ninja. The game allowed users to create their own levels and share them via QR code. Ninjahax was made by hacker smealum in 2014 by launching homebrew code and started the chain of vulnerability exploits to gain full access to the 3DS.