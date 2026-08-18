This cheatsheet catalogs the intermediate and advanced tools, commands, and cryptographic concepts you mastered across OverTheWire Bandit (0-22) and your introductory TryHackMe rooms.

[[Index_bandit]] -> Index for bandit
## 🔍 1. Advanced Filtering & System Searches

These tools are crucial for **Enumeration and Reconnaissance**—finding hidden assets, files with specific traits, and sorting massive data streams.

### `find` (Advanced Filtering)

Search for files based on precise file sizes, group owners, or users, while silently discarding system permission errors.

- **Command:** `find /path -type f -size 33c -user bandit7 -group bandit6 2>/dev/null`
    
- **Breakdown:**
    
    - `-type f`: Look only for files (not directories).
        
    - `-size 33c`: Look for a file of exactly `33` bytes (`c` stands for bytes).
        
    - `-user / -group`: Match explicit owners.
        
    - `2>/dev/null`: Redirects Standard Error stream (`2`) to a virtual black hole (`/dev/null`) so your screen doesn't flood with "Permission denied" errors.
        

### `grep` (Regular Expressions & Filtering)

Filters text streams using pattern matching.

- **Case-Insensitive Search:** `grep -i "password" data.txt`
    
- **Recursive search in all directory files:** `grep -ri "password" .`
    
- **Regex Anchor Match (Starts with):** `grep "^===" data.txt`
    
    - _Note:_ The `^` character forces grep to only return lines that _start_ with the pattern (e.g., lines starting with multiple equals signs).
        

### `sort` & `uniq` (Finding Unique Items)

Identify unique or repeating items in a cluttered text file.

- **Command:** `sort data.txt | uniq -u`
    
- **Breakdown:**
    
    - `sort`: Arranges lines alphabetically (required because `uniq` only detects consecutive identical lines).
        
    - `|`: Pipes the output straight to the next tool.
        
    - `uniq -u`: Filters the list to display **only** lines that appear exactly _once_ in the entire file.
        

## 📦 2. File Analysis & Reverse Engineering

Tools for inspecting binaries, converting hex dumps, and peeling back layered file compression.

### `strings` (Binary Inspection)

Extracts human-readable text strings from non-text files (binaries, databases, system files).

- **Command:** `strings data.txt`
    

### `file` (Genuine Type Check)

Looks at the internal "magic bytes" (headers) of a file to tell you what it _actually_ is, completely ignoring the file extension.

- **Command:** `file mystery_file`
    

### `xxd` (Hex Dumping and Reversing)

Converts raw binary data into hexadecimal text representation, and vice-versa.

- **Reverse a hex dump into binary:** `xxd -r source.txt > output_binary`
    

### Decompression Suite

Commands to strip away compression formats identified by the `file` command:

- **Gzip (.gz):** `gunzip -c compressed_file > output`
    
- **Bzip2 (.bz2):** `bunzip2 -c compressed_file > output`
    
- **Tar archive (.tar):** `tar -xf compressed_file` (Extracts files silently to your current folder).
    

## 🌐 3. Secure Remote Access & File Transfer

Protocols and tools for authenticating securely, copying files across networks, and managing raw private keys.

### SSH with Custom Ports & Keys

Log in using standard password auth or cryptographic key files.

- **Using a non-standard port:** `ssh user@host -p 2220`
    
- **Using a Private Key (Identity):** `ssh -i private_key.key user@host -p 2220`
    

### `scp` (Secure Copy Protocol)

Securely downloads files from a remote server down to your local machine.

- **Command (Run from your local terminal):** `scp -P 2220 user@host:/path/to/remote/file .`
    
    - _Crucial Flags:_ Use capital `-P` for SCP port mapping, and remember the trailing `.` to specify "download it right here".
        

### `icacls` (Windows Key File Lockdowns)

If Windows OpenSSH complains that your private key file permissions are "too open", run these PowerShell commands to strip global inheritances:

```
icacls .\sshkey.private /inheritance:r
icacls .\sshkey.private /grant:r "${env:USERNAME}:(R,W)"
```

## 🔌 4. Port Scanning & Connectivity

Tools used for mapping targets, opening raw connections, and communicating over secure sockets.

### `nmap` (Network Port Scanner)

Finds active systems on a network and maps out open doors (ports).

- **Command:** `nmap -Pn -p 31000-32000 -sV -n localhost`
    
- **Breakdown:**
    
    - `-Pn`: Treats the host as online, skipping host discovery ping filters.
        
    - `-p 31000-32000`: Scans a specific range of ports.
        
    - `-sV`: Determines the version/name of the service running on the port.
        
    - `-n`: Disables reverse DNS lookups to prevent connection hangs.
        

### `nc` (Netcat - Raw Sockets)

The "Swiss army knife" of networking. Connects to raw ports to transmit plain-text data or listen for incoming shells.

- **Connect to port:** `nc localhost 30000`
    

### `openssl s_client` (Encrypted Connections)

Connects to raw ports that enforce SSL/TLS encryption (which standard `nc` cannot communicate with).

- **Command:** `openssl s_client -connect localhost:30001`
    

### `ncat` (Upgraded Netcat)

Nmap's secure rewrite of Netcat. Supports native encryption and access control.

- **Secure chatroom host:** `ncat -lvp 4444 --ssl`
    
- **Secure chatroom client:** `ncat <host_ip> 4444 --ssl`
    

## 👑 5. Privilege Escalation & Automation

Mechanics for bypassing file restrictions, understanding automated tasks, and manipulating scripting engines.

### `setuid` (Set User ID Permissions)

A special permission bit that allows low-privilege users to execute a binary with the permissions of the file's owner (often `root`).

- **Visual indicator:** Lowercase `s` in owner execute field (`-rwsr-xr-x`).
    
- **Numeric value:** Prepend a `4` (e.g., `chmod 4755 script`).
    
- **Exploitation concept:** Find a misconfigured `setuid` binary and force it to read files it shouldn't, or trick it into spawning an administrative shell.
    

### `cron` (Automated Scheduled Tasks)

System daemon that executes scheduled shell scripts automatically.

- **Cron config folder:** `/etc/cron.d/`
    

### Bash Variable Expansion & Command Substitution

- **`$variable`**: Reads the value of a variable (e.g., `$whoami`).
    
- **`$(command)`**: Runs a command in-line, grabs the text output, and embeds it directly.
    
    - _Example:_ `echo "I am $(whoami)"` outputs `"I am bandit22"`.
        

### `md5sum` (Cryptographic Hashing)

Processes text strings through the MD5 algorithm to generate a deterministic, one-way 32-character hexadecimal fingerprint.

- **Command:** `echo "text" | md5sum`
    

## ⚡ 6. Under the Hood Shortcuts

- **`realpath <file>`**: Instantly returns the absolute, complete file system path of a file, bypassing directory structural lookups.
    
- **`script -a filename.log`**: Standard Linux terminal recorder. Captures every input and output command you run and commits it cleanly to a local log file.