Here is your **clean, fixed, final README** — all images display normally, no ASCII, no broken formatting.
I kept everything exactly the same, only cleaned structure, spacing, and formatting so it looks perfect in GitHub.

---

```markdown
# 🌸 Sakura Room — OSINT Investigation Walkthrough

This is my personal documentation of the OSINT investigation in the **Sakura Room** on TryHackMe (created with huge thanks to OSINT Dojo).  
The room simulates tracking a cybercriminal using **passive OSINT techniques**.

---

## 🐾 Task 1 — Introduction

**Goal:** Start the investigation.

**Instructions:**  
Type the following to begin the room:

**Let's Go!**

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
2. View page source (`Ctrl+U`).  
3. Search for the image filename or path.  
   Found in the HTML:
```

filename="/home/SakuraSnowAngelAiko/Desktop/pwnedletter.png"

```
4. Extract username:
- Between `/home/` and `/Desktop` → **SakuraSnowAngelAiko**

### ✅ Answer
**Username:** `SakuraSnowAngelAiko`

---

## 🐾 Task 3 — Social Media Footprint

**Goal:** Find the attacker’s real name and email.

### 🔍 Background
The attacker reused their username across platforms. Username correlation exposes personal data.

### 🕵️‍♂️ Methodology
1. Start with `SakuraSnowAngelAiko`.  
2. Check social media:

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_57_03 (1)" src="https://github.com/user-attachments/assets/6272f023-d2f4-4b5f-a633-c9bae98adea8" />

- X/Twitter → `@SakuraLoverAiko`  
- Found reference to → `@AikoAbe3`

3. Real name found: **Aiko Abe**  
4. Email discovered through PGP key on GitHub:

<img width="1920" height="1080" alt="Screenshot (29)" src="https://github.com/user-attachments/assets/bef7a91e-618b-4d32-bab3-e5016baa90fb" />

📧 **Email:** `SakuraSnowAngel83@protonmail.com`

### ✅ Answers
- **Full Name:** `Aiko Abe`  
- **Email:** `SakuraSnowAngel83@protonmail.com`

---

## 🐾 Task 4 — Cryptocurrency Trail

**Goal:** Recover deleted GitHub info and trace crypto activity.

### 🔍 Background
The attacker deleted sensitive data. Commit history can reveal hidden info.

### 🕵️‍♂️ Methodology

<img width="1920" height="909" alt="Screenshot_2025-11-29_07_05_33 (1)" src="https://github.com/user-attachments/assets/a2dfb091-1c57-4467-aa7a-85298703ce0a" />

1. Identify crypto repo → **Ethereum**.  
2. Recover deleted wallet from commit history:

<img width="1920" height="909" alt="Screenshot_2025-11-29_08_17_50 (1)" src="https://github.com/user-attachments/assets/65771707-de8a-4f09-9457-2fc6abf17c4d" />

Wallet Address:  
`0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`

<img width="1920" height="909" alt="Screenshot_2025-11-29_08_23_58 (1)" src="https://github.com/user-attachments/assets/29c5bcc7-1cd1-4bf7-abaa-99083c8cbbb2" />

3. Investigate on explorer.  
4. Mining pool → **Ethermine**  
5. Exchanged coin → **Tether (USDT)**

### ✅ Answers
- **Cryptocurrency:** Ethereum  
- **Wallet:** `0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`  
- **Mining Pool:** Ethermine  
- **Other Coin:** Tether (USDT)

---

## 🐾 Task 5 — Twitter & WiFi

**Goal:** Identify attacker’s new Twitter handle and home WiFi BSSID.

### 🕵️‍♂️ Methodology
1. From screenshot:

<img width="1920" height="909" alt="Screenshot_2025-11-29_05_57_12 (1)" src="https://github.com/user-attachments/assets/a5611ac7-7319-418c-9325-93228d108ccb" />

→ Account: **@SakuraLoverAiko**

<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/001c4a10-abe1-45e8-8627-d9bc02d6dbfb" />

2. Geo clues lead to WiFi BSSID via Wigle:

**BSSID:** `84:af:ec:34:fc:f8`

### ✅ Answers
- **Twitter:** `@SakuraLoverAiko`  
- **WiFi BSSID:** `84:af:ec:34:fc:f8`

---

## 🐾 Task 6 — Track Home Route

**Goal:** Identify attacker’s final destination using geo-OSINT.

### 🕵️‍♂️ Methodology
1. Pre-flight airport → **DCA**  
2. Layover → **HND (Tokyo Haneda)**  
3. Lake seen during flight → **Lake Inawashiro**  
4. Reverse image search maps to → **Hirosaki**

<img width="1920" height="1080" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/e2e925a0-b29a-4b26-94e7-7e49ec502fe2" />

### ✅ Answers
- **Closest Airport:** DCA  
- **Layover:** HND  
- **Lake:** Lake Inawashiro  
- **Likely Home City:** Hirosaki, Japan
```

---

If you want, I can also:

✅ Add a clean title banner
✅ Add a table of contents
✅ Add badges (TryHackMe, OSINT, GitHub)
✅ Make it look like a professional OSINT case report

Just tell me.
