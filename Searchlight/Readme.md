
# 🔦 Searchlight — OSINT / IMINT Case Report

**TryHackMe Walkthrough • Image Intelligence • Geolocation**

> **Note:** AI tools, such as Gemini or reverse‑image assistants, are **game‑changing** in the field of OSINT. They accelerate image recognition, geolocation, and contextual analysis, allowing investigators to extract critical information faster while validating findings through traditional methods.

---

## 🧭 Overview

This report documents the full investigation of the **Searchlight** room on TryHackMe. The challenge focuses on **IMINT/GEOINT** techniques: extracting visual clues from images and video, performing geolocation, validating locations using OSINT tools, and answering context questions based on real‑world intelligence.

Skills used:

* Image analysis & pattern recognition
* Reverse image search (Google, Bing, Gemini)
* Geolocation via Google Maps & Street View
* Identifying landmarks, signs, languages, domains, and contextual clues
* Research through Wikipedia and official business pages
* Verification of addresses, owners, contact details, and metadata

---

## 🏷️ Case Summary

| Field      | Details                                                       |
| ---------- | ------------------------------------------------------------- |
| Room Name  | Searchlight                                                   |
| Category   | OSINT / IMINT / GEOINT                                        |
| Goal       | Geolocate all images & video and answer context questions     |
| Methods    | Reverse image search, Google Maps, Wikipedia, business lookup |
| Difficulty | Beginner OSINT / IMINT                                        |

---

# 🐾 Task 1 — Understanding the Flag Format

**Answer:** `sl{ready}`

Task required understanding that all flags must be submitted in the format `sl{answer}`.

---

# 🐾 Task 2 — First Geolocation Challenge

**Goal:** Identify the street shown in the provided image.

### 🔍 Process

* Performed reverse image search on the photo.
* Recognized recognizable architecture and street layout from London.
* Confirmed using Google Maps Street View.

### 🎯 Result

* **Street Name:** `sl{carnaby street}`

---

# 🐾 Task 3 — Tube Station Identification

Image contained London Underground signage.

### 🔍 Process

1. Reverse‑searched the image → identified it as part of the **Piccadilly Line**.
2. Used Google Images + Wikipedia to confirm station name and historical data.
3. Retrieved opening year and number of platforms from the station’s page.

### 🎯 Findings

| Question            | Answer                  |
| ------------------- | ----------------------- |
| City                | `sl{london}`            |
| Tube station        | `sl{piccadilly circus}` |
| Opening year        | `sl{1906}`              |
| Number of platforms | `sl{4}`                 |

---

# 🐾 Task 4 — Airport Identification

Image included banners ending in **“.ca”**, hinting Canada.

### 🔍 Process

1. Noticed `.ca` domain → confirmed country.
2. Reverse search revealed the interior of **Vancouver International Airport**.
3. Verified location via airport website and Google Maps.

### 🎯 Findings

| Question | Answer                                |
| -------- | ------------------------------------- |
| Building | `sl{vancouver international airport}` |
| Country  | `sl{canada}`                          |
| City     | `sl{richmond}`                        |

---

# 🐾 Task 5 — Coffee Shop Geolocation

A café storefront located in Scotland.

### 🔍 Process

1. Attempted multiple image searches; no direct hit.
2. Noticed regional architectural style → searched Scotland manually.
3. Located matching storefront on Google Maps → Blairgowrie.
4. Found exact address on their business page.
5. Extracted phone number, email, and owners’ surname.

### 🎯 Findings

| Question        | Answer                         |
| --------------- | ------------------------------ |
| City            | `sl{blairgowrie}`              |
| Street          | `sl{allan street}`             |
| Phone           | `sl{+447878 839128}`           |
| Email           | `sl{theweecoffeeshop@aol.com}` |
| Owners’ surname | `sl{cochrane}`                 |

---

# 🐾 Task 6 — Famous Restaurant Identification

### 🔍 Process

* Reverse image searched interior shot.
* Matched iconic styling to **Katz’s Delicatessen**, New York.
* Looked up related media.
* Found that *Andrew Knowlton* from Bon Appétit worked 24 hours there.

### 🎯 Findings

| Question   | Answer                |
| ---------- | --------------------- |
| Restaurant | `sl{katz's deli}`     |
| Editor     | `sl{andrew knowlton}` |

---

# 🐾 Task 7 — Statue Identification

### 🔍 Process

* Reverse image search → identified the chrome sculpture **“Rudolph the Chrome Nosed Reindeer.”**
* Original image credited to photographer **Kjersti Stensrud**.

### 🎯 Findings

| Question     | Answer                                  |
| ------------ | --------------------------------------- |
| Statue name  | `sl{rudolph the chrome nosed reindeer}` |
| Photographer | `sl{kjersti stensrud}`                  |

---

# 🐾 Task 8 — Video Geolocation (Final Challenge)

### 🔍 Process

1. Analyzed skyline and key architectural structures in the video.
2. Identified the unique dome‑shaped “boat‑like” building.
3. Used AI + manual verification to match it to Singapore’s waterfront.
4. Cross‑referenced with nearby hotel lists.
5. Found matching structure near **Novotel Singapore Clarke Quay**.

### 🎯 Finding

* **Hotel:** `sl{novotel singapore clarke quay}`

---

# 🧩 Final Conclusion

The **Searchlight** room demonstrates practical IMINT/GEOINT workflows:

✔ Using visual clues (signs, language, architecture)
✔ Reverse searching images accurately
✔ Validating results through official sources, maps, and business pages
✔ Extracting contextual metadata (owners, emails, dates)
✔ Applying OSINT discipline to real‑world imagery

**AI tools proved extremely useful** for accelerating identification and verification, making the OSINT workflow faster and more reliable.

All objectives were completed, and each location was correctly geolocated using open‑source intelligence techniques.
