
#  RootMe – CTF Investigation Log

## 🧾 Overview

This document records my investigation while working through the *RootMe* machine.
It focuses on reconnaissance, initial access, and privilege escalation paths discovered during analysis.

---

## 🧠 Initial State

I began with basic service enumeration to understand the exposed attack surface of the machine.

The goal at this stage was to identify entry points through web or network services.

---

## 🔍 Reconnaissance

A full port scan revealed two primary services:

* HTTP (web service)
* SSH (remote access)

The presence of a web service suggested that initial exploitation would likely occur through the HTTP interface.

---

## 🌐 Web Service Analysis

The Apache version identified on the target was:

* Apache 2.4.41

SSH was confirmed running on port 22, indicating standard remote login capability.

At this stage, I focused on web enumeration due to its higher probability of exposing vulnerabilities in CTF environments.

---

## 📂 Directory Enumeration

Directory brute-force enumeration was performed against the web server.

The scan revealed multiple endpoints:

* `/panel`
* `/uploads`

Among these, the main hidden directory identified as relevant was:

* `/panel`

This indicated the presence of an administrative or functional interface not exposed on the main page.

---

## 🚪 Web Upload Functionality

Inside the application, an upload feature was discovered.

The upload handling was partially filtered, but not fully secured.

This created an opportunity to bypass restrictions by modifying file type extensions.

Through testing different approaches, a PHP-based upload bypass was identified.

This allowed execution on the server side and resulted in a successful shell connection.

---

## 💻 Initial Shell Access

After successful exploitation of the upload functionality, a reverse shell was established.

From there, user-level access was achieved on the system.

The `user.txt` file was located in the web directory (`/var/www`).

The file contained:

* `THM{y0u_g0t_a_sh3ll}`

This confirmed successful initial access to the machine.

---

## 🧭 Privilege Escalation Enumeration

Post-exploitation enumeration focused on identifying misconfigurations and privilege escalation vectors.

SUID files were enumerated across the system.

Among the results, a notable binary was identified:

* `/usr/bin/python2.7`

This binary stood out due to its executable permissions and known misuse potential in privilege escalation scenarios.

---

## 🔐 Privilege Escalation Path

Using known exploitation techniques for misconfigured SUID binaries, the Python binary was leveraged to escalate privileges.

This resulted in root-level access to the system.

At this stage, system control was fully achieved.

---

## 🎯 Root Access Outcome

After privilege escalation, the root directory was accessed.

The final flag was retrieved:

* `THM{pr1v1l3g3_3sc4l4t10n}`

---

## 📉 Reflection Notes

### Key observations:

* Web upload functionality was the primary entry point
* File extension handling was insufficiently secured
* SUID misconfiguration provided a direct privilege escalation path
* Enumeration of system binaries was critical for escalation discovery

### Challenges faced:

* Initial reliance on external assistance for SUID identification
* Limited familiarity with exploitation paths using Python SUID
* Difficulty confirming privilege level at early root stage
