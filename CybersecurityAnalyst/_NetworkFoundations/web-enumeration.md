# Web Enumeration

**Quick Short Description:**  
Digging into web servers on ports 80/443 to find hidden directories, subdomains, and juicy info like credentials or admin panels.

---

## Summary

Once I find a web server during service scanning, it's worth enumerating hard — web apps are a huge attack surface. The main tool here is **GoBuster**, which can brute-force directories/files (`dir` mode) and DNS subdomains (`dns` mode). Directory enumeration with a wordlist like `common.txt` reveals hidden paths — status codes matter: 200 = OK, 403 = forbidden (but exists), 301 = redirect (also exists). I found a WordPress install at `/wordpress` that was still in setup mode, which could lead to RCE.

For subdomains, `gobuster dns -d <domain> -w <wordlist>` found several interesting ones like `blog.`, `customer.`, `my.`, and `ns1/2/3.` for `inlanefreight.com`.

Other quick wins:
- **Banner grabbing / headers** — `curl -IL` shows `Server:` headers revealing Apache/nginx versions and frameworks.
- **WhatWeb** — fingerprints web servers, frameworks, and apps (even scan a whole /24 with `--no-errors`).
- **EyeWitness** — screenshots and fingerprints web apps, checks default creds.
- **SSL/TLS certificates** — can leak company names and email addresses (useful for phishing if in scope).
- **robots.txt** — often lists private/admin paths it tries to hide from crawlers (e.g., `/private`, `/uploaded_files`).
- **Source code** — `CTRL+U` sometimes reveals developer comments with test credentials.

---

## What I Did

- Ran `gobuster dir -u http://10.10.10.121/ -w /usr/share/seclists/Discovery/Web-Content/common.txt` and found `/.hta`, `/.htpasswd`, `/.htaccess` (403), `/index.php` (200), `/server-status` (403), and `/wordpress` (301).
- Visited `/wordpress` and saw it was still in setup mode — potential RCE.
- Used `gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt` and found `blog`, `customer`, `my`, `ns1`, `ns2`, `ns3` subdomains.
- Ran `curl -IL https://www.inlanefreight.com` to grab headers — revealed Apache/2.4.29 (Ubuntu) and WordPress API links.
- Ran `whatweb 10.10.10.121` — identified Apache 2.4.41, Ubuntu, and PHP 7.4.3 phpinfo page. Also tested `whatweb --no-errors 10.10.10.0/24` to fingerprint multiple hosts at once.
- Checked `robots.txt` on the target — found disallowed entries `/private` and `/uploaded_files`; navigating to `/private` revealed an admin login page.
- Viewed page source (`CTRL+U`) and found a developer comment with test account credentials.

---

## What I Learned

- **GoBuster is versatile** — `dir` mode for hidden paths, `dns` mode for subdomains. Status codes tell you a lot: 403/301 still mean the resource exists.
- **WordPress (and CMSs in general)** are massive attack surfaces, especially if left in setup mode.
- **Subdomain enumeration** can uncover admin panels or extra functionality not linked from the main site.
- **Headers and whatweb** give quick tech fingerprints (server, framework, versions) that map to known vulns.
- **Certificates** can leak org info and emails — useful for phishing or just understanding the target.
- **robots.txt is not security** — it literally points to the private stuff.
- **Always check source code** — developers leave comments, credentials, and hidden endpoints all the time.
- Enumeration is about layering: directories → subdomains → headers → source → certs. Each step feeds the next.