# Gobuster Enumeration Modes – Commands, Purpose & Examples

This document provides a structured overview of the **Gobuster tool**, covering its three main modes: **dns**, **dir**, and **vhost**. For each mode, the **purpose**, **required flags**, **optional flags**, and **example commands** are explained clearly. Hands-on usage is emphasized to reflect real-world reconnaissance scenarios.

---

## 1. Gobuster DNS Mode

### Purpose
DNS mode is used to **enumerate subdomains** of a given domain. It helps identify additional entry points such as admin portals, test environments, or legacy services that may not be directly visible.

### How It Works
- Uses **DNS resolution** to test potential subdomains
- Combines a target domain with a wordlist
- Valid subdomains are identified when DNS records resolve successfully

### Required Flags
- `-d` : Target domain
- `-w` : Wordlist for subdomain names
- `dns` : Enables DNS mode

### Common Optional Flags
- `-t` : Number of threads
- `--timeout` : DNS query timeout
- `-o` : Output file

### Example Command
```bash
gobuster dns -d example.com -w subdomains.txt -t 50
```

### Example Use Case
Finding hidden subdomains such as:
- `admin.example.com`
- `dev.example.com`
- `api.example.com`

---

## 2. Gobuster Directory (Dir) Mode

### Purpose
Dir mode is used to **discover hidden directories and files** on a web server. This helps locate sensitive paths such as admin panels, configuration files, or backups.

### How It Works
- Sends HTTP requests to a target URL
- Appends wordlist entries as paths
- Identifies valid responses based on HTTP status codes

### Required Flags
- `-u` : Target URL
- `-w` : Wordlist for directories/files
- `dir` : Enables directory mode

### Common Optional Flags
- `-x` : File extensions (e.g., php, txt, html)
- `-t` : Number of threads
- `-o` : Output file
- `-s` : Specific status codes to include

### Example Command
```bash
gobuster dir -u http://example.com -w common.txt -x php,txt
```

### Example Use Case
Discovering:
- `/admin/`
- `/login.php`
- `/backup.zip`

---

## 3. Gobuster VHost Mode

### Purpose
VHost mode is used to **enumerate virtual hosts** on a web server. This is useful when multiple websites are hosted on the same IP address.

### How It Works
- Sends **HTTP requests** to the target URL
- Modifies the `Host` header using a wordlist
- Identifies valid virtual hosts based on server responses

### Required Flags
- `-u` : Target URL
- `-w` : Wordlist for virtual host names
- `vhost` : Enables virtual host mode

### Common Optional Flags
- `-t` : Number of threads
- `-o` : Output file
- `--append-domain` : Appends domain name to wordlist entries

### Example Command
```bash
gobuster vhost -u http://example.com -w vhosts.txt --append-domain
```

### Example Use Case
Finding hidden applications such as:
- `admin.example.com`
- `test.example.com`
- `internal.example.com`

---

## Difference Between Subdomains and Virtual Hosts

| Feature | Subdomains (DNS Mode) | Virtual Hosts (VHost Mode) |
|------|----------------------|----------------------------|
| Resolution Method | DNS-based | HTTP-based |
| Dependency | Requires DNS record | Depends on web server configuration |
| Scan Technique | DNS queries | Web requests with Host header |

---

## Practical Application

At the end of each task, the learned concepts were **applied through hands-on exercises**, enabling:
- Better understanding of enumeration techniques
- Real-time command execution
- Analysis of scan results in practical environments

---

## Command Breakdown Examples

Below are detailed breakdowns of the Gobuster commands used in practical enumeration exercises. Each flag is explained with its purpose to improve clarity and understanding.

---

### 1️⃣ Gobuster VHost Mode Command

```bash
gobuster vhost -u "http://10.80.187.26" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

#### Breakdown of Flags
- `gobuster vhost` : Runs Gobuster in **virtual host enumeration mode**
- `-u "http://10.80.187.26"` : Target IP address hosting multiple virtual hosts
- `--domain example.thm` : Base domain name to test virtual hosts against
- `-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` : Wordlist containing potential virtual host names
- `--append-domain` : Appends the domain name to each wordlist entry (e.g., `admin.example.thm`)
- `--exclude-length 250-320` : Filters out responses with content lengths between 250 and 320 bytes to reduce false positives

#### Purpose
This command is used to **identify hidden virtual hosts** configured on the same IP address that are not publicly listed in DNS.

---

### 2️⃣ Gobuster DNS Mode Command

```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

#### Breakdown of Flags
- `gobuster dns` : Runs Gobuster in **DNS subdomain enumeration mode**
- `-d example.thm` : Target domain for subdomain discovery
- `-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` : Wordlist containing possible subdomain names

#### Purpose
This command performs **DNS-based subdomain enumeration** to discover valid subdomains such as development, admin, or API endpoints.

---

### 3️⃣ Gobuster Directory (Dir) Mode Command

```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js
```

#### Breakdown of Flags
- `gobuster dir` : Runs Gobuster in **directory and file enumeration mode**
- `-u "http://www.example.thm"` : Target web application URL
- `-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` : Wordlist for directory and file names
- `-x .php,.js` : Checks for files with `.php` and `.js` extensions

#### Purpose
This command is used to **discover hidden directories and files** on the web server that may expose sensitive functionality.

---

## Conclusion

Understanding the breakdown of Gobuster commands and flags allows precise and efficient enumeration. Correct usage of filters, domains, and extensions significantly improves scan accuracy and reduces noise during reconnaissance.

