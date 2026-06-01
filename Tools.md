# Tools Reference – Digital Forensics

Quick reference for all tools used or encountered in this investigation.

---

## 🔧 Investigation Tools

### Autopsy 4.23.0
- **Type:** Open-source digital forensics platform
- **Used for:** Primary analysis — file system browsing, artifact extraction, keyword search, timeline, deleted file recovery
- **Download:** https://www.autopsy.com/
- **Key features used:**
  - PhotoRec Carver (file carving from unallocated space)
  - Keyword Search module
  - Timeline Analysis
  - Web Artifacts (history, cookies, bookmarks)
  - Recent Documents & Run Programs artifacts
  - Deleted file detection (red X icons)

### FTK Imager
- **Type:** Forensic imaging and verification tool by Exterro
- **Used for:** Verifying disk image integrity (MD5 hash check)
- **Download:** https://www.exterro.com/ftk-imager
- **Note:** Free to use, industry standard for image acquisition

### Surfshark
- **Type:** Commercial VPN and antivirus
- **Used for:** Scanning carved executable files for malware signatures
- **Result:** Detected TR/W32.Trojan in one of the carved files

---

## 🚨 Malicious / Suspicious Tools Found on the Disk Image

These are tools that were **found on the suspect's device** — not tools we used.

### NetStumbler
- **Type:** Wireless network scanner (wardiving tool)
- **Purpose:** Discovers nearby Wi-Fi networks including hidden SSIDs
- **Relevance:** Confirms wireless network reconnaissance activity

### Ethereal (now Wireshark)
- **Type:** Packet sniffer / network protocol analyzer
- **Purpose:** Captures and inspects network traffic in real time
- **Relevance:** Found alongside an interception file containing captured HTTP traffic

### Cain & Abel
- **Type:** Password recovery / cracking tool for Windows
- **Purpose:** Recovers passwords via sniffing, brute force, dictionary attacks
- **Relevance:** Directly linked to credential theft objectives

### John the Ripper
- **Type:** Password cracking tool (open source)
- **Source files found:** `cracker.c`, `best.c` in `My Documents`
- **Relevance:** 357 keyword hits for "john" — source code suggests intentional installation

### fping
- **Type:** Network scanning / ping utility
- **Purpose:** Rapidly pings multiple hosts to map a network
- **Relevance:** Used for network reconnaissance

### Pandora
- **Type:** Referenced in timeline activity
- **Relevance:** Associated with password cracking / network tools

### Anonymizer
- **Type:** Anonymizing software
- **Path found:** `D:\Drivers\Anonymizer`
- **Relevance:** Anti-forensic intent — hiding identity or traffic

### GhostWare
- **Type:** Stealth/anonymizing software
- **Relevance:** Artifacts found, accessed around 20 August 2004

### WinPcap
- **Type:** Packet capture library for Windows
- **Relevance:** Download confirmed in web browser history — required by Ethereal/Cain & Abel

---

## 📦 File Types & Artifacts Reference

| Artifact Type | What it tells you |
|---------------|------------------|
| `.lnk` (shortcut files) | Recently accessed files/folders — found in Recent Documents |
| Prefetch files | Programs that were executed — found in Run Programs |
| Unallocated space | Areas where deleted files may still exist |
| Browser history | Sites visited, downloads made |
| Web cookies | Sessions, logins, site interactions |
| Registry hives | System config, user activity, installed software |
| MFT (Master File Table) | NTFS metadata — file creation, modification, access times |

---

## ⏱️ MACB Timestamps Explained

| Letter | Stands for | Meaning |
|--------|-----------|---------|
| M | Modified | Last time file content was changed |
| A | Accessed | Last time file was opened/read |
| C | Created | When the file entry was created |
| B | Entry Modified | When the MFT record itself was last changed |

> Inconsistencies in MACB timestamps can indicate **timestomping** (anti-forensic timestamp manipulation).
