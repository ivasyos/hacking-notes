
# 🌐 VSFTPD 2.3.4 Backdoor — Penetration Test Report

Internal Network Exploitation • Metasploitable 2 Case Study

---

## 🧭 Overview

This report documents the complete exploitation of the **VSFTPD 2.3.4 backdoor** on a Metasploitable 2 machine within an internal lab network.
The objective was to demonstrate:

* Host discovery
* Service enumeration
* Vulnerability identification
* Metasploit exploitation
* Shell access confirmation

This assessment simulates a real-world situation where an outdated and compromised FTP service leads to full system compromise.

---

## 🏷️ Case Summary

| Field               | Details                               |
| ------------------- | ------------------------------------- |
| Case Name           | VSFTPD 2.3.4 Backdoor Exploitation    |
| Testing Environment | Internal Lab (Kali + Metasploitable2) |
| Target IP           | *Discovered during scan*              |
| Vulnerable Service  | FTP (vsftpd 2.3.4)                    |
| Vulnerability Type  | Backdoor → Remote Code Execution      |
| Exploitation Tool   | Metasploit Framework                  |
| Result              | Successful shell with root access     |

---

## 🐾 Task 1 — Network Identification

**Goal:** Identify attacker subnet and scan the network.

### Evidence
<img width="1920" height="909" alt="Screenshot_2025-12-02_06_31_52" src="https://github.com/user-attachments/assets/9d30e4d5-3a86-49e3-94ed-f30b99a46db4" />
Screenshot: `ip a` output
Screenshot: Nmap network sweep

### Analysis

* Used `ip a` to determine active interface and subnet.
* Performed a ping sweep to enumerate all active devices:

```bash
nmap -sn <subnet>/24
```

* One host matched typical Metasploitable fingerprints (multiple open ports, lack of firewall).

### 🎯 Finding

**Target Identified:** Metasploitable 2 host located on the network.

---

## 🐾 Task 2 — Service Enumeration

**Goal:** Enumerate open services and detect vulnerable versions.

### Evidence
<img width="1920" height="909" alt="Screenshot_2025-10-20_07_07_13" src="https://github.com/user-attachments/assets/6dbc708c-e19f-4af8-9657-913ad75de07e" />

Screenshot: Nmap `-A` scan results

### Analysis

Executed:

```bash
nmap -A <target-ip>
```

Key discovery:

* **Port 21/tcp — vsftpd 2.3.4**
* This version is known to contain an intentional backdoor inserted into a compromised code mirror.
* Backdoor triggers when the FTP username ends with `:)`.

### 🎯 Finding

**Vulnerability Confirmed:** vsftpd 2.3.4 (Backdoored)

---

## 🐾 Task 3 — Exploit Discovery (Metasploit)

**Goal:** Locate the appropriate exploit module.

### Evidence

Screenshot: Metasploit search results

### Analysis

Inside Metasploit:

```bash
search vsftpd
```

Returned module:

```
exploit/unix/ftp/vsftpd_234_backdoor
```

This module automatically triggers the malicious backdoor and spawns a shell on TCP port 6200.

### 🎯 Finding

**Exploit Available:** vsftpd_234_backdoor

---

## 🐾 Task 4 — Exploitation

**Goal:** Execute the exploit and obtain system access.

### Evidence

Screenshots:
<img width="1920" height="909" alt="Screenshot_2025-12-02_06_37_24" src="https://github.com/user-attachments/assets/455e422f-1a2b-4f05-bcce-06bf162b3aac" />

* Exploit configuration
* Successful shell creation

### Analysis

Configured the target:

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS <target-ip>
run
```

The backdoor activated successfully, opening a root shell.

Verification:

```bash
id
uname -a
```

Output confirmed **uid=0(root)**.

### 🎯 Findings

* **Exploitation Successful**
* **Shell Access:** Obtained
* **Privilege Level:** Root

---

## 🐾 Task 5 — Impact Assessment

**Goal:** Determine the severity and potential damage.

### Analysis

If deployed in a real environment, this vulnerability would allow:

* Full system compromise
* Unrestricted command execution
* Lateral movement inside the network
* Installation of persistent backdoors
* Access to confidential files

This is a **critical security failure**.

### 🎯 Finding

**Impact:** Complete compromise of the target system.

---

## 🐾 Task 6 — Remediation

**Goal:** Define actionable security recommendations.

### Recommendations

✔ Upgrade VSFTPD to a secure version
✔ Disable anonymous FTP access
✔ Restrict FTP to internal, trusted hosts only
✔ Replace FTP with SFTP/SSH
✔ Implement routine version scanning & patch management

### 🎯 Finding

**Risk Mitigated with proper upgrades and service hardening.**

---

## 🧩 Final Conclusion

The assessment demonstrated that the outdated and backdoored **VSFTPD 2.3.4** service on Metasploitable 2 could be exploited with minimal effort, resulting in full root access via a remote shell.

The exploitation chain included:

✔ Network discovery
✔ Service fingerprinting
✔ Vulnerability identification
✔ Metasploit exploitation
✔ Root-level system takeover

This case reinforces the importance of maintaining updated software, verifying service integrity, and enforcing strong patch management procedures.

