```markdown
# 🌸 Sakura Room — OSINT Investigation Walkthrough

This is my Personal documentation of my OSINT investigation in the Sakura Room on TryHackMe, created by Huge thanks for OSINT Dojo.  
The room simulates tracking a cybercriminal using passive OSINT techniques.

---

## 🐾 Task 1 — Introduction

**Goal:** Start the investigation.

**Instructions:**  
Type the following to begin the room:

Let's Go!


**Notes:**  
- This task is the entry point for the investigation.  
- All following tasks build on this.

---

## 🐾 Task 2 — Tip Off

**Goal:** Identify the attacker’s username.

### 🔍 Background
A static image was left behind by the attacker. Inspecting the page may reveal metadata containing the attacker’s identity.

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_53_13" src="https://github.com/user-attachments/assets/d24f1a7c-0493-4016-919e-20ace0eb5486" />


### 🕵️‍♂️ Methodology (Passive OSINT Only)
1. Open the page with the attacker’s image.  
2. View page source (`Ctrl+U` or right-click → *View Page Source*).  
3. Search for the image filename or path.  
   - Found in the HTML:  
     ```
     filename="/home/SakuraSnowAngelAiko/Desktop/pwnedletter.png"
     ```
4. Extract the username from the path:  
   - Text between `/home/` and `/Desktop` → **SakuraSnowAngelAiko**

### ✅ Answer
**Username:** `SakuraSnowAngelAiko`

---

## 🐾 Task 3 — Social Media Footprint

**Goal:** Find the attacker’s full real name and email using their username.

### 🔍 Background
The attacker reused their username across multiple platforms. Username correlation can expose real personal information.

### 🕵️‍♂️ Methodology
1. Start with the username: `SakuraSnowAngelAiko`.  
2. Search social media platforms:

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_57_03 (1)" src="https://github.com/user-attachments/assets/6272f023-d2f4-4b5f-a633-c9bae98adea8" />
 
   - X/Twitter → `https://x.com/SakuraLoverAiko`

   - Found reference to another account: `@AikoAbe3`  
3. Confirm account consistency and collect information:  
   - Real name found: **Aiko Abe**  
4. Find email in public artifacts (GitHub PGP key):  
<img width="1920" height="1080" alt="Screenshot (29)" src="https://github.com/user-attachments/assets/bef7a91e-618b-4d32-bab3-e5016baa90fb" />


[SakuraSnowAngel83@protonmail.com](mailto:SakuraSnowAngel83@protonmail.com)



### ✅ Answers
- **Full real name:** `Aiko Abe`  
- **Email address:** `SakuraSnowAngel83@protonmail.com`

---

## 🐾 Task 4 — Cryptocurrency Trail

**Goal:** Recover deleted GitHub information and trace cryptocurrency activity.

### 🔍 Background
The attacker edited or deleted information in their GitHub repos to hide data. Commit history can reveal valuable clues.

### 🕵️‍♂️ Methodology
<img width="1920" height="909" alt="Screenshot_2025-11-29_07_05_33 (1)" src="https://github.com/user-attachments/assets/a2dfb091-1c57-4467-aa7a-85298703ce0a" />

1. Identify cryptocurrency repo → **Ethereum**.  
2. Check GitHub commit history to recover deleted wallet:
<img width="1920" height="909" alt="Screenshot_2025-11-29_08_17_50 (1)" src="https://github.com/user-attachments/assets/65771707-de8a-4f09-9457-2fc6abf17c4d" />

0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef


<img width="1920" height="909" alt="Screenshot_2025-11-29_08_23_58 (1)" src="https://github.com/user-attachments/assets/29c5bcc7-1cd1-4bf7-abaa-99083c8cbbb2" />

3. Investigate the wallet using Ethereum explorer.  
4. Identify mining pool: **Ethermine** (payment received Jan 23, 2021 UTC).  
5. Identify exchanged cryptocurrency: **Tether (USDT)**.

### ✅ Answers
- **Cryptocurrency:** Ethereum  
- **Wallet Address:** `0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`  
- **Mining Pool:** Ethermine  
- **Other Cryptocurrency:** Tether (USDT)

---

## 🐾 Task 5 — Twitter & WiFi

**Goal:** Identify the attacker’s current Twitter handle and home WiFi BSSID.

### 🔍 Background
The attacker messaged OSINT Dojo using a different Twitter account, potentially revealing more personal info.

### 🕵️‍♂️ Methodology
1. Examine screenshot and identify the Twitter handle:
<img width="1920" height="909" alt="Screenshot_2025-11-29_05_57_12 (1)" src="https://github.com/user-attachments/assets/a5611ac7-7319-418c-9325-93228d108ccb" />
- **`@SakuraLoverAiko`**

<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/001c4a10-abe1-45e8-8627-d9bc02d6dbfb" />

2. Analyze images posted for geolocation clues (map of home).  
3. Use **Wigle Advanced Search** to confirm BSSID:  
- **`84:af:ec:34:fc:f8`**

### ✅ Answers
- **Twitter Handle:** `@SakuraLoverAiko`  
- **Home WiFi BSSID:** `84:af:ec:34:fc:f8`

---

## 🐾 Task 6 — Track Home Route

**Goal:** Use photos and geolocation to identify the attacker’s final destination and route.

### 🔍 Background
Photos on Twitter reveal flight paths, airports, and local landmarks. OSINT synthesis helps identify “home.”

### 🕵️‍♂️ Methodology
1. Reverse image search airport before flight → **DCA (Ronald Reagan Washington National Airport)**  
2. Reverse image search last layover → **HND (Tokyo Haneda Airport)**  
3. Identify lake from final flight photo → **Lake Inawashiro**  
4. Reverse image search final hotel → **Hirosaki**

### ✅ Answers
- **Closest Airport (before flight):** DCA  
- **Last Layover Airport:** HND
<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/e2e925a0-b29a-4b26-94e7-7e49ec502fe2" />

- **Lake visible on flight:** Lake Inawashiro  
- **Likely Home City:** Hirosaki, Japan

:

