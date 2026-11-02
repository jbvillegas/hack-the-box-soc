# Service Scanning

**Quick Short Description:**  
Intro to finding open ports, identifying services, and poking at them to see what info I can pull.

---

## Summary

This section is all about figuring out what's running on a target machine before trying to attack it. Every service on a computer talks over a port (1-65,535, with the low ones reserved for privileged services), and manually checking all of them would be insane — so we use **Nmap** to automate port scanning.

A basic `nmap <ip>` scan hits the top 1,000 most common ports and tells you which ones are open, what state they're in (open, closed, filtered), and a guess at the service name. To get more detail, I can use:
- `-sV` → version scan (fingerprints the service, app name, and version)
- `-sC` → runs default Nmap scripts for extra info
- `-p-` → scans all 65,535 TCP ports

That combo gives way more info but takes much longer. The version info is gold — it can reveal the OS (e.g., OpenSSH version pointing to Ubuntu 20.04) and possible vulnerabilities.

From there, I learned about **banner grabbing** (connecting to a service and reading its self-identification banner — via Netcat or `nmap --script=banner`), and then actually interacting with services:

- **FTP (21)** — check for anonymous login; if allowed, browse directories and download files that might contain credentials.
- **SMB (445)** — huge attack surface on Windows; use `smbclient -L` to list shares, `smb-os-discovery.nse` for OS info, and connect with credentials to grab files like `passwords.txt`.
- **SNMP (161)** — default community strings like `public`/`private` are often unchanged; `snmpwalk` and `onesixtyone` can pull system info and even credentials.

---

## What I Did

- Ran a basic `nmap 10.129.42.253` and found ports 21, 22, 80, 139, 445 open.
- Ran `nmap -sV -sC -p- 10.129.42.253` to get full versions — identified vsftpd 3.0.3, OpenSSH 8.2p1 on Ubuntu, Apache 2.4.41, and Samba smbd 4.6.2.
- Cross-referenced the OpenSSH version to pin down Ubuntu 20.04 Focal Fossa.
- Banner grabbed FTP with `nc -nv 10.129.42.253 21` → confirmed vsFTPd 3.0.3.
- Connected to FTP anonymously, browsed to `pub/`, downloaded `login.txt`, and found credentials: `admin:ftp@dmin123`.
- Ran `smbclient -N -L \\10.129.42.253` to list shares (`print$`, `users`, `IPC$`).
- Tried guest access on `users` → access denied. Retried with `bob:Welcome1` → success, downloaded `passwords.txt` from `\bob\`.
- Used `snmpwalk -v 2c -c public 10.129.42.253` to confirm the hostname `gs-svcscan`.

---

## What I Learned

- **Nmap is the go-to** for port scanning, and flags like `-sV`, `-sC`, and `-p-` drastically change what you learn — but also how long the scan takes.
- **Version numbers are clues** — they can identify the OS and point to known CVEs (e.g., EternalBlue on legacy Windows 7 SMB).
- **Banner grabbing** is a quick, cheap way to fingerprint a service, whether manually with Netcat or automated with Nmap scripts.
- **FTP anonymous access** is still a thing and can leak credentials or files.
- **SMB shares** are worth enumerating carefully — guest access may fail, but valid credentials can open up sensitive files.
- **SNMP default community strings** (`public`, `private`) are often left unchanged and can expose a ton of system info.
- Enumeration is iterative — one finding (like a credential file) can unlock the next step.