
# 🌸 **Sakura Room — OSINT Case Report**

### **Passive OSINT Investigation • TryHackMe Walkthrough**

---

## 🧭 Overview

This report documents my complete OSINT investigation of the **Sakura Room** on TryHackMe, created with support from **OSINT Dojo**.
The scenario simulates tracking a cybercriminal using **passive OSINT techniques only**.

The report includes:

* Username enumeration
* Social media identity correlation
* Cryptocurrency wallet tracing
* Metadata analysis
* WiFi & geolocation intelligence
* Travel pattern reconstruction

---

# 🏷️ **Case Summary**

| Field                    | Details                                                                     |
| ------------------------ | --------------------------------------------------------------------------- |
| **Case Name**            | Sakura OSINT Investigation                                                  |
| **Target Alias**         | SakuraSnowAngelAiko                                                         |
| **Real Name**            | Aiko Abe                                                                    |
| **Primary Handle**       | @SakuraLoverAiko                                                            |
| **Email**                | [SakuraSnowAngel83@protonmail.com](mailto:SakuraSnowAngel83@protonmail.com) |
| **Main Cryptocurrency**  | Ethereum                                                                    |
| **Wallet Address**       | `0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`                                |
| **Home BSSID**           | `84:af:ec:34:fc:f8`                                                         |
| **Likely Home Location** | Hirosaki, Japan                                                             |

---

# 🐾 **Task 1 — Introduction**

**Goal:** Start the investigation.

No technical analysis; this task simply unlocks the room.

---

# 🐾 **Task 2 — Tip Off**

**Goal:** Identify the attacker’s username.

### Evidence

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_53_13" src="https://github.com/user-attachments/assets/d24f1a7c-0493-4016-919e-20ace0eb5486" />

### Analysis

Source code of the page contains the image path:

```
/home/SakuraSnowAngelAiko/Desktop/pwnedletter.png
```

Extracted username: **SakuraSnowAngelAiko**

### 🎯 Finding

**Username:** `SakuraSnowAngelAiko`

---

# 🐾 **Task 3 — Social Media Footprint**

**Goal:** Identify real name and email.

### Evidence

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_57_03 (1)" src="https://github.com/user-attachments/assets/6272f023-d2f4-4b5f-a633-c9bae98adea8" />

### Analysis

* Username reused on multiple platforms
* Connected handle found: **@AikoAbe3**
* Real identity correlated: **Aiko Abe**

PGP key on GitHub revealed email:

<img width="1920" height="1080" alt="Screenshot (29)" src="https://github.com/user-attachments/assets/bef7a91e-618b-4d32-bab3-e5016baa90fb" />

### 🎯 Findings

* **Real Name:** `Aiko Abe`
* **Email:** `SakuraSnowAngel83@protonmail.com`

---

# 🐾 **Task 4 — Cryptocurrency Trail**

**Goal:** Trace the attacker’s cryptocurrency activity.

### Evidence

<img width="1920" height="909" alt="Screenshot_2025-11-29_07_05_33 (1)" src="https://github.com/user-attachments/assets/a2dfb091-1c57-4467-aa7a-85298703ce0a" />

### Analysis

Commit history revealed a deleted Ethereum wallet:

<img width="1920" height="909" alt="Screenshot_2025-11-29_08_17_50 (1)" src="https://github.com/user-attachments/assets/65771707-de8a-4f09-9457-2fc6abf17c4d" />

Wallet:
`0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`

Further blockchain investigation:

<img width="1920" height="909" alt="Screenshot_2025-11-29_08_23_58 (1)" src="https://github.com/user-attachments/assets/29c5bcc7-1cd1-4bf7-abaa-99083c8cbbb2" />

* Mining pool payment from **Ethermine**
* Conversion to **USDT (Tether)** observed

### 🎯 Findings

* **Currency:** Ethereum
* **Wallet Address:** `0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`
* **Mining Pool:** Ethermine
* **Converted Currency:** USDT (Tether)

---

# 🐾 **Task 5 — Twitter & WiFi Identification**

**Goal:** Identify attacker’s Twitter handle and home WiFi.

### Evidence

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_57_12 (1)" src="https://github.com/user-attachments/assets/a5611ac7-7319-418c-9325-93228d108ccb" />

<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/001c4a10-abe1-45e8-8627-d9bc02d6dbfb" />

### Analysis

* New handle identified → **@SakuraLoverAiko**
* Image metadata + Wigle lookup revealed WiFi BSSID:

`84:af:ec:34:fc:f8`

### 🎯 Findings

* **Twitter Handle:** `@SakuraLoverAiko`
* **Home BSSID:** `84:af:ec:34:fc:f8`

---

# 🐾 **Task 6 — Travel & Home Location**

**Goal:** Determine the attacker’s route and home city.

### Analysis Steps

1. **Airport before flight:** DCA (Ronald Reagan Washington National Airport)
2. **Layover:** HND (Tokyo Haneda Airport)
3. **Lake in photo:** Lake Inawashiro
4. **Hotel / final area:** Hirosaki

### Evidence

<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/e2e925a0-b29a-4b26-94e7-7e49ec502fe2" />

### 🎯 Findings

* **Closest Airport:** DCA
* **Layover Airport:** HND
* **Lake Seen:** Lake Inawashiro
* **Likely Home City:** Hirosaki, Japan

---

# 🧩 Final Conclusion

The OSINT investigation successfully unmasked the attacker through:

✔ Username analysis
✔ Social media cross-correlation
✔ Metadata extraction
✔ Blockchain tracing
✔ WiFi geolocation
✔ Travel-route reconstruction

The attacker **Aiko Abe**, operating under the alias **SakuraSnowAngelAiko**, was linked to cryptocurrency mining, multiple social profiles, and a likely residence in **Hirosaki, Japan**.

---

