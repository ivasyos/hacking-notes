
# 🚀 TakeOver — Subdomain Takeover Case Report

TryHackMe Walkthrough • Subdomain Enumeration • DNS Misconfiguration

## 🧭 Overview

This report documents the exploitation of the **TakeOver** room on TryHackMe.
The challenge focuses on discovering misconfigured DNS entries that lead to a **subdomain takeover**, allowing an attacker to serve malicious content.

Techniques used:

* Host mapping
* Subdomain enumeration
* Certificate analysis
* DNS inspection
* Identifying takeover‑ready subdomains

---

## 🏷️ Case Summary

| Field          | Details                                    |
| -------------- | ------------------------------------------ |
| Room Name      | TakeOver                                   |
| Target Domain  | `futurevera.thm`                           |
| Target IP      | `10.66.162.207`                            |
| Goal           | Identify the takeover‑vulnerable subdomain |
| Attack Surface | Misconfigured DNS / orphaned subdomain     |
| Flag           | `flag{beea0d6edfcee06a59b83fb50ae81b2f}`   |

---

# 🐾 Task — Identify Takeover Vulnerability

**Goal:** Determine which part of the site is vulnerable to a subdomain takeover.

### 1️⃣ Add Domain to `/etc/hosts`

Before scanning:

```bash
sudo nano /etc/hosts
```

Add:

```
10.66.162.207   futurevera.thm
```

This maps the domain locally.

---

# 🐾 Reconnaissance

### 2️⃣ Nmap Scan (Open Ports + Service Info)

```bash
nmap -A 10.66.162.207
```

Findings:

* **22/tcp** — OpenSSH
* **80/tcp** — Apache web server
* **443/tcp** — HTTPS enabled
* Redirects to: `https://futurevera.thm/`

Nothing directly useful yet.

---

# 🐾 Subdomain Investigation

### 3️⃣ Enumerate Subdomains

Using Gobuster:

```bash
gobuster vhost -u https://futurevera.thm -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

Result: **No useful hits**.

### 4️⃣ Identify Certificate Clues

Visiting `https://futurevera.thm`, check the **SSL certificate details**.

Inside the certificate (CN + SAN fields), you observe:

```
commonName = futurevera.thm
organizationName = Futurevera
```

But more importantly, the certificate reveals an **additional subdomain** reference:

```
*.futurevera.thm
```

Or sometimes specifically:

```
support.futurevera.thm
```

This is the key hint:
The company previously had a support subdomain — now removed or unconfigured → perfect for takeover.

---

# 🐾 Confirming the Subdomain Issue

### 5️⃣ Browser Check

Visit:

```
https://support.futurevera.thm
```

The page fails to load correctly.

### 6️⃣ Error Behavior Indicates Takeover Potential

Typical indicators:

* DNS returns the domain → but no server configured
* HTTPS fails or shows certificate mismatch
* Browser displays: *Could not resolve host / SSL error*

This misconfiguration means the subdomain **exists in DNS** but is **unclaimed in hosting** → vulnerable to takeover.

This is exactly what the challenge wanted.

---

# 🐾 Final Flag

When the misconfigured subdomain is correctly worked through, the challenge reveals the flag:

```
flag{beea0d6edfcee06a59b83fb50ae81b2f}
```

---

# 🧩 Final Conclusion

The **TakeOver** room demonstrates a classic **subdomain takeover** scenario caused by poor DNS hygiene.

✔ Domain mapped locally
✔ Subdomain enumeration attempted
✔ Certificate inspection revealed the hidden subdomain
✔ Unsupported subdomain = takeover‑ready
✔ Flag successfully retrieved

This highlights the importance of:

* Cleaning unused DNS records
* Securing wildcard DNS entries
* Monitoring unclaimed subdomains
* Ensuring certificates match active infrastructure
