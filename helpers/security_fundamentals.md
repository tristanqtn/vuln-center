# Security Fundamentals

# Cryptography: An Evolving Art

**Cryptography:** Conception of algorithm
**Cryptanalysis:** the analysis of an algorithm

The objective of cryptography is to protect an information and allow only
autorized user to access it.

To do so, it must be a 2 ways operation : **Encryption & Decryption**

## From Past to Present

- First cryptography algorithm: **Scytale (X to VII century bf. JC)**

  - A strip of paper is wrap around a cylinder
  - The encrypted message is written on the paper around the cylinder
  - And then you remove the cylinder and send it to your contact
  - To decrypt the message, the right cylinder is needed.
  - This kind of algorithm are called “Permutation algorithm”

- Substitution: **Cesar Code, Vigenère Algo, Rotation Algo**
  - substitution algorithm, substitute a letter by another one or a symbol
  - for Cesar code the whole alphabet was shifted using an offset: Bonjour => ERQMRXU
  - Marie Stuart's code: substitute a letter by a symbol
  - Subsitution algorithm are weak to an attack called “Frequency Analysis”. This attack is base on the frenquency of each letters in a certain language. For exemple in French the letter “e” is the most used the it’s “A” ….

Some algorithms used both methods such as the Enigma code.

## Modern Cryptographic Techniques

### Kerckoffs Principles

- Fundamental principle of cryptography
  - The encryption and decryption methods (the algorithms) must (can) be
    made public.
  - Only the parameterization of the algorithms must be kept secret.
- Security rely on the complexity of solving a mathematical problem
  (algorithmic, complexity theory)
- Key
  - Parameter of a cryptographic mechanism whose knowledge separates
    legitimate users from opponents.
  - Must be sufficiently variable so that an attacker cannot not list all the
    possible keys: sufficient size and random selection of keys
  - Key: role similar to a password

### Symmetric vs. Asymmetric Cryptography

#### **Symmetric:** Security is based on the sharing of a secret between legitimate users.

One example of Symmetric algorithm is Vernam algorithm. Encryption algorithm consisting in performing XOR bit by bit between the clear and the key, as long as the message is generated random and single-use. The Vernam algorithm is almost perfect, impossible de decrypt if you
don’t know the key, even with infinite computation power.

Encryption : ENCRYPTED = MESSAGE xor KEY

Decryption : MESSAGE = ENCRYPTED xor KEY

**Problems:**

- The key must be the same size as the message
- The key must be use only one time
- If the key is used even twice, the code is broken

One way to remove the size problem in Vernam algorithm is to “cut” the
plain text in multiple block of the size of the key. The key is generated
with a Pseudo random generator.

**Examples:** DES, AES, hashing algorythms (here the key is public, the hashed message is the same for a given file and has the same size has the key)

#### **Asymmetric:** Asymmetric cryptography refers to encryption methods using the

principle of a Public key and a Private Key.

The public key is used to cipher the data and the private key is used to
uncipher the message.

- The security of Asymmetric algorithm rely on the knowledge of a secret
  by a legitimate user and the distribution of a key related to the secret to
  other users.
- Encrypting and decrypting are two opposite operations but "being
  capable of encryption" should not imply "capable of decipher"
  - Everyone must be able to encrypt with the public key.
  - Only the holder of the private key can decrypt
  - The size of the key is link to the complexity of the algorithm

Bob wants to send a message to Alice. Bob cyphers the message with Alice's public key. This message can only be decyphered with Alice's secret key that she keeps secret.

**Examples:** RSA, DSA, ECDSA, used for encryption of messages, hashes, authentication, key exchange, ...

# Network Security Fundamentals

## Understanding Firewalls and VPNs

A firewall is software and/or hardware that enforces the network security policy, which defines what types of communications are allowed on that computer
network. It monitors and controls applications and data (packet) flows.

- **Stateless:** equipment that processes each request independently, without relation to previous request. Filtering is based on a set of rules that define the filtering policy.

- **Statefull:** check the conformity of packets to a current connection. That is, they check that each packet in a connection is a continuation of the previous packet and the response to a packet in the other direction. They also know how to intelligently filter ICMP packets that are used to signal IP flows.

- **Application Firewall (Proxy):** present on the application layer, the requests are processed by dedicated processes, for example an Http request will be filtered by an Http proxy process. The firewall will reject all requests that do not conform to the protocol specifications.

- **Web Application Firewall (WAF):** A Web Application Firewall (WAF) is a type of firewall that protects the web application server in the backend against various attacks. The WAF ensures that the security of the web server is not compromised by examining HTTP / HTTPS request packets and web traffic patterns.

## Network Architectures

**VLAN (Virtual Local Area Network):** used to create virtual groups of devices in order to isolate them in a network.

**DMZ (Demilitarized Zone):** This part of the network is used to expose some services or application to the internet. The goal is to restrict access between private VLANs and the DMZ. If the DMZ is compromised the other VLANs aren't impacted. Traffic from DMZ to the internal network are strictly forbidden, all traffic must come from the internal network

### Intrusion Detection

To help you detect and block internal attack (malware or intrusion) you can implement Intrusion Detection System (IDS: only detect attacks on a network. When an attack is detected, an alert is sent to the security teams) or Intrusion Prevention System (IPS: automatically block malicious activities on a network).

## Network Attack and Defense Strategies

**DoS (Undistributed Denial of Service)**: Undistributed denial of service attacks can be countered by identifying the IP address of the attacking machine and banning it at the firewall or server level. IP packets from the hostile machine are then rejected unprocessed, preventing the server's service from becoming saturated and going offline.

**DDoS (Distributed Denial of Service):** sending multiple requests to the attacked web resource in order to hinder the website's ability to handle requests and block its operation. Unfortunately, there is no miracle solutions against DDOS attack.

**ARP Spoofing/Poisoning:** allows the attacker to hijack communication flows passing between a target machine and a gateway. The attacker can then listen, modify or even block network packets. This attack can allow an attacker to be in a "Man In The Middle" position on the network.

In general, networking is based on trust. The ARP request and response scenario is organized so that the first response to the ARP request is accepted and recorded. In ARP spoofing, hackers attempt to get ahead of the target computer by sending a response containing incorrect information in order to manipulate the ARP table of the computer sending the request.

Protections: static ARP tables, encrypt all communications and check TLS certificate validity. IDS and IPS can also help.

# Pentest Procedure

A penetration is an authorized simulated cyber attack performed to evaluate the security of a system. A penetration test is limited in:

- **time:** the test has a beginning and ending date that must be respected.
- **resources:** you will use your own tool and infrastructure but attackers could use a much bigger infrastructure / tools to hack a client
- **scope:** a pentest is limited to the scope defined with the client, nothing more

---

Type of pentest:

- **White Box:** all information (accounts, URLS), you have access to the source code, you can talk with the devs, ...
- **Grey Box:** few information, you may have an account (user, admin, ...) or even an admin access
- **Black Box:** no information about the system, no account nor admin access, the only information you have are the one available online (attacker position)

## Steps of a Pentest

**Footprinting/Reconnaissance:** Passive: gather information about the target system, network, or organization. This is the first step in the pentest process and involves collecting as much information as possible about the target (OSINT).

**Scanning:** involves identifying live hosts, open ports, and services running on those ports. This step is crucial for identifying potential entry points into the target system.

**Enumeration:** involves gathering information about the target system, such as user accounts, network shares, and other system details. This step is essential for understanding the target system's configuration and potential vulnerabilities.

**Penetration:** involves exploiting identified vulnerabilities to gain access to the target system. This step is where the actual attack occurs, and the pentester attempts to gain unauthorized access to the target system.

**Privilege Escalation:** involves gaining higher levels of access within the target system. This step is crucial for demonstrating the potential impact of a successful attack and identifying additional vulnerabilities.

**Cleaning/Covering Tracks:** involves removing evidence of the attack from the target system. This step is essential for maintaining the stealth of the attack and avoiding detection.

**Reporting:** involves documenting the findings of the pentest and providing recommendations for improving the target system's security. This step is crucial for communicating the results of the pentest to the target organization and ensuring that vulnerabilities are addressed.

## Secure Coding and Application Security

Using the OWASP (Open Web Application Security Project) TOP 10 (regularly-updated report outlining security concerns for web application security, focusing on the 10 most critical risks) you can assert the security level of your web app.

**XSS (Cross Site Scripting):** is a type of injection where an attacker will put malicious HTML or JavaScript code in a data use by the application (form, URL parameter, etc.) often used for defacing and data exfiltration (session theft).

- **Reflected XSS:** Input from a user is directly returned to the browser, permitting injection of arbitrary content
- **Stored XSS:** Input from a user is stored on the server (often in a database) and returned later without proper escaping,

Solution: do not interpret user input as code but has simple content (char)

**SQL Injection:** is a vulnerability that occur when the developer use the user input as a direct parameter for an SQL query. The attacker can then inject SQL code in the input to modify the query and access the database.

Solution: use prepared statement or ORM (Object Relational Mapping)

Risk: data exfiltration, data modification, data deletion, ...

```bash
# example
" or 1=1; --
```

**CSRF (Cross Site Request Forgery):** is an attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker's choosing.

Risk: data modification, data deletion, ...

Solution: use a token to validate the request

**Weak Authentication:** weak password, no 2FA, no password policy, default password, ...

Solution: use strong password, 2FA, password policy, ...

**Local File Inclusion (LFI) and Remote File Inclusion (RFI):** is a vulnerability that allows an attacker to include files on a server through the web browser. This vulnerability occurs when a web application includes a file without correctly sanitizing the input, allowing an attacker to manipulate the input and inject path traversal characters.

Risk: data exfiltration, data modification, data deletion, ...

Solution: use a whitelist of authorized files, define a root directory for the webserver to prevent path traversal

**Path Traversal:** is a vulnerability that allows an attacker to access files and directories that are stored outside the web root folder. By manipulating variables that reference files with “dot-dot-slash (../)” sequences and its variations, or by using absolute file paths, an attacker can access unauthorized files and directories.

Risk: data exfiltration, data modification, data deletion, ...

Solution: use a whitelist of authorized files, define a root directory for the webserver to prevent path traversal

**Insecure File Upload:** is a vulnerability that allows an attacker to upload and execute malicious scripts on a web server. This vulnerability occurs when a web application allows the user to upload files to the server without proper validation of the file type and content.

Risk: data exfiltration, data modification, data deletion, ...

Solution: validate the file type and content, never execute an uploaded file, check magic number, store the file in a secure location, ...

Classify a vulnerability:

**Availability:** is the ability of a system to provide a service to its users. An attack on availability is an attack on the system's ability to function properly.

**Integrity:** is the trustworthiness of data. An attack on integrity is an attack on the trustworthiness of data.

**Confidentiality:** is the protection of data from unauthorized access. An attack on confidentiality is an attack on the protection of data from unauthorized access.

**Traceability/Authenticity:** is the ability to verify the identity of a person or process. An attack on authenticity is an attack on the ability to verify the identity of a person or process.

### Penetration Testing Insights

Refers to tools documentation available here: [Tools](./tools.md)

## Post-Exploitation Techniques and System Hardening

Depending of the scope of your audit, you can still go further after compromising a server. Once you gain access to a system or a server, you can have a lot more servers to compromise on your scope.

Check rights, cron tasks, env variables, writable files of the current user:

```bash
whoami
id
sudo -l
sudo su
ps aux | grep root
find /etc/ -writable -type f 2>/dev/null
crontab -l; ls -alh /var/spool/cron; ls -al /etc/ | grep cron; ls -
cat /etc/profile; cat /etc/bashrc; cat ~/.bash_profile; cat ~/.bashrc; cat ~/.bash_logout; env;
```

Check for Kernel vulnerabilities:

```bash
uname -a
cat /etc/issue
cat /etc/*-release
cat /proc/version
```

SUID and GUID files:

SUID (Set User ID) and SGID (Set Group ID) are special permissions that can be set on executable files. They are used to allow users to execute a file with the permissions of the file owner or group owner, respectively.

```bash
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null
```

# Secure Code Practices

## Authentication hardening and Mechanisms

**Authentication:** is the process of verifying the identity of a user or process. It is a fundamental security measure that helps protect systems and data from unauthorized access.

**Authorization:** is the process of determining what actions a user or process is allowed to perform. It is a fundamental security measure that helps protect systems and data from unauthorized access.

**Identification:** is the process of associating a user or process with a unique identifier. It is a fundamental security measure that helps protect systems and data from unauthorized access.

## Buffer Overflow

A buffer overflow occurs when a program writes more data to a buffer than the buffer can hold. This can result in the overwriting of adjacent memory locations, leading to a crash or the execution of arbitrary code.

**Stack-based buffer overflow:** occurs when a program writes more data to a stack buffer than the buffer can hold. This can result in the overwriting of the return address on the stack, leading to the execution of arbitrary code.

**Heap-based buffer overflow:** occurs when a program writes more data to a heap buffer than the buffer can hold. This can result in the overwriting of adjacent heap memory, leading to a crash or the execution of arbitrary code.

**Format string vulnerability:** occurs when a program uses user input as the format string for a printf or similar function. This can result in the leaking of memory contents or the execution of arbitrary code.

**Integer overflow:** occurs when a program performs an arithmetic operation that results in an integer value that is too large to be represented. This can result in the corruption of memory or the execution of arbitrary code.

**Memory leak:** occurs when a program allocates memory but does not free it when it is no longer needed. This can result in the exhaustion of system resources or the execution of arbitrary code.

**Race conditions:** occurs when a program performs an operation that depends on the timing of other operations. This can result in the corruption of memory or the execution of arbitrary code. Solution: use mutex, semaphore, ...

## Audit Trail and logging

**Audit trail:** is a record of system activity that can be used to monitor and analyze the behavior of users and processes. It is a fundamental security measure that helps protect systems and data from unauthorized access.

**Logging:** is the process of recording system activity to a log file. It is a fundamental security measure that helps protect systems and data from unauthorized access.

**Log analysis:** is the process of reviewing log files to identify security events and potential security issues. It is a fundamental security measure that helps protect systems and data from unauthorized access.
