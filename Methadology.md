# Investigation Methodology – NIST CFReDS Hacking Case

## Objective
Identify evidence of unauthorized system access and hacking activity on a forensic disk image attributed to user "Mr. Evil" (Greg Schardt).

---

## Phase 1 – Evidence Acquisition & Integrity Verification

- Obtained the disk image in EnCase (.E01) format
- Loaded into Autopsy 4.23.0 as a new case
- Verified image integrity using MD5 hash: `aee4fcd9301c03b3b054623ca261959a`
- Disabled Plaso ingest module to speed up triage phase
  - Reason: Plaso significantly increases processing time; better run separately on a dedicated machine in real investigations

**Ingest modules enabled:**
- Interesting Files Identifier
- Central Repository
- PhotoRec Carver ✅ (critical for deleted file recovery)
- Virtual Machine Extractor
- Data Source Integrity
- Android Analyzer (aLEAPP)
- DJI Drone Analyzer
- YARA Analyzer
- iOS Analyzer (iLEAPP)
- GPX Parser

---

## Phase 2 – File System Analysis

- Explored full directory tree starting from root
- Looked for non-standard folders, hidden directories, and unusual naming
- Noted files in `Temp/` created/modified within a 90-minute window — indicates burst of activity
- Autopsy red X icons = deleted files not yet overwritten → recoverable as evidence
- Total deleted files on volume: **7,145**

**Key directories examined:**
- `C:\Documents and Settings\Mr. Evil\` — primary user profile
- `C:\Documents and Settings\Mr. Evil\My Documents\` — John the Ripper source files here
- `C:\WINDOWS\Temp\` — high file activity in short period
- `D:\Drivers\Anonymizer\` — referenced in Recent Documents

---

## Phase 3 – Artifact Examination

Focused on two artifact categories:
1. **Recent Documents** — shows what files the user accessed recently
2. **Run Programs** — shows what executables were launched (Prefetch data)

**Notable artifacts found:**
- Shortcut to `D:\Drivers\Anonymizer` — anonymizing software accessed
- GhostWare artifacts — accessed around 20 August 2004
- Hex pane used to validate paths and metadata in .lnk shortcut files

---

## Phase 4 – Keyword Searches

| Keyword | Hits | Significance |
|---------|------|-------------|
| `john` | 357 | John the Ripper source files (cracker.c, best.c) in My Documents |
| `password` | ~1,900 | Concentrated in user profile — password cracking activity |
| `metasploit` | — | Searched for exploitation framework traces |

> John the Ripper files are intentionally installed tools — not accidental. Combined with 7,145 deleted files, this strongly suggests active password-cracking use.

---

## Phase 5 – File Export & Malware Analysis

- Exported suspicious files from forensic image to a separate analysis folder
- Did NOT alter the original evidence (forensic best practice)
- Ran exported `.exe` files through antivirus (Surfshark)

**Results:**
- 4 files flagged as suspicious
- 1 confirmed: **TR/W32.Trojan**
- Files recovered from unallocated space via PhotoRec Carver
- Location: `C:\Users\...\Hacking Case\ModuleOutput\PhotoRec Carver\`

> Files in unallocated space = previously deleted. Suggests an attempt to remove evidence.

---

## Phase 6 – Timeline Analysis

- Used Autopsy's built-in Timeline module
- Set view to logarithmic scale to handle large event count variance

**Timeline summary:**

| Date | Event |
|------|-------|
| 19 August 2004 | OS installed |
| 20 August 2004 | GhostWare artifacts, multiple tools installed |
| 20–27 August 2004 | Heavy activity in My Documents, tool usage |
| 27 August 2004 | Last system shutdown |

- Activity span: **~8 days**
- All suspicious artifacts attributed to the `Mr. Evil` account
- Tools confirmed active during this window: Pandora, Cain & Abel, fping, NetStumbler, Ethereal

---

## Forensic Principles Followed

- ✅ Original image never modified
- ✅ MD5 hash verified before and after
- ✅ All findings documented with file paths, timestamps, and MD5 hashes
- ✅ Screenshots taken at key stages
- ✅ Exported files kept separate from source image
- ✅ Plaso disabled for triage speed, noted for reproducibility
