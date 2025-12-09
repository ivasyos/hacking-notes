
# 🌐 OhSINT — OSINT Case Report

Open-Source Intelligence • TryHackMe Case Study

---

## 🧭 Overview

This report documents the complete **OSINT investigation** of the **OhSINT room** on TryHackMe. The goal was to extract information about a target using only publicly available data and metadata from a single image file.

Key objectives included:

* Metadata extraction
* Social media investigation
* Public repository search
* Correlating findings to answer specific questions

This assessment simulates a real-world scenario where minimal digital traces can reveal sensitive personal information.

---

## 🏷️ Case Summary

| Field               | Details                         |
| ------------------- | ------------------------------- |
| Case Name           | OhSINT OSINT Challenge          |
| Testing Environment | Kali Linux / TryHackMe          |
| Target Data         | Single image file               |
| Vulnerability Type  | Information Exposure / OSINT    |
| Tools Used          | `exiftool`, Google, GitHub, X   |
| Result              | Complete identification of user |

---

## 🐾 Task 1 — Metadata Extraction

**Goal:** Analyze the image for hidden information.

### Evidence

```bash
exiftool target_image.jpg
```

**Findings from metadata:**

* Username: `OWoodflint`
* Associated social links: X and GitHub accounts

### 🎯 Finding

**Metadata provided a direct lead** to the target’s social profiles.

---

## 🐾 Task 2 — Social Media Investigation

**Goal:** Explore public posts for information disclosure.

### Evidence

* X (Twitter) profile: `@OWoodflint`
* Key post examples:

  * “From my house I can get free wifi ;D BSSID: B4:5D:50:AA:86:41”
  * “Hello world!”

### Analysis

* BSSID revealed possible network SSID through lookup: `UnileverWiFi`
* Avatar analysis: Cat image

### 🎯 Findings

* **User avatar:** Cat
* **City of residence:** London
* **Connected WAP SSID:** UnileverWiFi

---

## 🐾 Task 3 — GitHub Investigation

**Goal:** Identify additional personal information from repositories.

### Evidence

* GitHub profile: `OWoodflint`
* Email address found in project README: `OWoodflint@gmail.com`

### 🎯 Findings

* **Personal email:** [OWoodflint@gmail.com](mailto:OWoodflint@gmail.com)
* **Website reference:** [https://oliverwoodflint.wordpress.com](https://oliverwoodflint.wordpress.com)

---

## 🐾 Task 4 — Holiday & Location Tracking

**Goal:** Determine user travel and location info.

### Evidence

* Website post: “Hey, I’m in New York right now, so I will update this site right away with new photos!”

### 🎯 Finding

* **Current location / holiday:** New York

---

## 🐾 Task 5 — Password Discovery

**Goal:** Extract the user’s password from publicly available code.

### Evidence

* GitHub source code revealed password in a search snippet: `pennYDr0pper.!`

### 🎯 Finding

* **User password:** pennYDr0pper.!

---

## 🧩 Final Conclusion

Through **careful OSINT techniques**, the investigation uncovered the following sensitive information from minimal data:

✔ User’s real name / handle: OWoodflint
✔ City of residence: London
✔ SSID of WAP: UnileverWiFi
✔ Personal email: [OWoodflint@gmail.com](mailto:OWoodflint@gmail.com)
✔ Current holiday location: New York
✔ Password: pennYDr0pper.!

This exercise demonstrates how **exposed metadata and public profiles** can compromise privacy, reinforcing the need for cautious online behavior.
