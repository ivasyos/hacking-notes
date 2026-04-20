```md
# Break Out The Cage – CTF Investigation Log

## 🧾 Overview
This document records my investigation while working through the “Break Out The Cage” machine. It focuses on reconnaissance, initial access, decoding/forensics steps, and privilege escalation paths discovered during the challenge.

---

## 🧠 Initial State
I started the machine with basic enumeration to understand what services were exposed and what entry points could exist.

The main goal at this stage was to find anything that could lead to initial access or hidden data leaks.

---

## 🔍 Reconnaissance
A full nmap scan revealed multiple services running on the target:

- SSH
- FTP (anonymous login enabled)
- HTTP (web service)

The most interesting service at the start was FTP because it allowed anonymous access and contained files that looked like they might hide useful data.

---

## 📂 FTP Investigation
Inside the FTP service, I found files containing encoded data.

The content appeared to be Base64 encoded, so I attempted decoding it.

After decoding, the output still looked like another layer of encoded or transformed text, not a final readable result.

At this point, I struggled to fully interpret it and used external AI assistance to help decode the remaining structure.

The decoded result eventually led to a phrase:

> “Wrap Eekcl - The quick brown fox jumps over the lazy dog!!! Sfw. (etc.)”

This suggested there was further transformation or hidden meaning behind the text.

---

## 👤 Username Discovery
During investigation, I found references to a user named:

- Weston

This information was initially obtained through external walkthrough reference, since I did not yet fully understand the hidden structure of the challenge (especially mp3/steganography-related parts).

---

## 🔐 Credential Discovery
Another Base64 encoded string was decoded and resulted in the word:

- vintage

This helped connect pieces of the puzzle and eventually led to full credentials:

### 🧑 Username:
Weston

### 🔑 Password:
Mydadisghostrideraintthatcoolnocausehesonfirejokes

---

## 🚪 Initial Access
Using the credentials, I successfully gained access to the machine.

However, I was unable to immediately locate or read `user.txt`, so I continued enumeration for privilege escalation paths.

---

## 🔎 Privilege Escalation Enumeration
During post-exploitation enumeration, I noticed a recurring message appearing in the terminal every few minutes.

This suggested a scheduled task or background process.

I investigated:

- cron jobs
- sudo misconfigurations
- SUID binaries

---

## ⚙️ SUID Discovery
While checking SUID binaries, I discovered:

- policykit (polkit)

I checked its version:

- version 0.105

After researching known vulnerabilities, I identified:

- CVE-2021-4034 (PwnKit)

This is a known privilege escalation vulnerability affecting polkit.

---

## 💥 Exploitation
I was not familiar with writing the exploit in C, so I used AI assistance to understand and generate working exploit code.

After compiling and transferring the exploit to the target machine using `wget`, I executed it successfully.

This resulted in root access.

---

## 🧾 User Flag
After escalation, I accessed the system files and found:

```

THM{M37AL_0R_P3N_T35T1NG}

```

---

## 🎯 Root Flag Discovery
After gaining root access, I explored the root directory.

Inside a backup email directory, I found two files:

- email1
- email2

Reading `email2` revealed the final flag:

```

THM{8R1NG_D0WN_7H3_C493_L0N9_L1V3_M3}

```

---

## 📉 Reflection Notes

### What worked well:
- FTP anonymous access was an important entry point
- Base64 decoding revealed hidden clues
- SUID enumeration was key for privilege escalation
- CVE research directly led to root access

### Mistakes / weaknesses:
- I relied on walkthroughs for username discovery
- I used AI assistance for decoding and exploit creation
- Limited knowledge of steganography and C-based exploits slowed progress
- I missed some clues during initial enumeration

### Key learning:
- Enumeration is everything in CTFs
- SUID binaries are critical escalation targets
- CVE research is powerful when combined with system version checking
- Even if tools or AI are used, understanding the process is important for growth
```
