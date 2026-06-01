# Key Findings Summary – NIST CFReDS Hacking Case

**Case:** NIST CFReDS Hacking Case Investigation (2004)  
**Suspect:** Greg Schardt / alias "Mr. Evil"  
**Device:** Dell CPi Laptop (Serial No. VLQLW)  
**Activity Window:** 19–27 August 2004 (~8 days)

---

## 🔴 Critical Evidence

### 1. Confirmed Hacking Tools Installed
| Tool | Category | Status |
|------|----------|--------|
| NetStumbler | Wireless scanner / wardriving | Present on disk |
| Ethereal | Packet sniffer | Present on disk |
| Cain & Abel | Password recovery / sniffing | Present on disk |
| John the Ripper | Password cracker | Source code in My Documents |
| 123 Write All Stored Passwords | Credential dumper | Present on disk |
| fping | Network scanner | Referenced in timeline |
| Anonymizer | Anti-forensic / anonymizing | Accessed via Recent Documents |
| GhostWare | Stealth software | Artifacts present |

### 2. Malware Recovered
- **4 executable files** flagged by antivirus
- **1 confirmed Trojan:** TR/W32.Trojan (file: f1616389.exe)
- Recovered from **unallocated space** via PhotoRec Carver
- Suggests files were deleted but not securely wiped

### 3. Active Network Interception Evidence
- Interception file containing **captured HTTP traffic** found on disk
- **WinPcap** download confirmed in web browser history (required for packet capture tools)
- Wireless PCMCIA card + homemade 802.11b antenna found with device

### 4. Password Cracking Activity
- John the Ripper source files (`cracker.c`, `best.c`) in `My Documents`
- **357 keyword hits** for "john" across disk image
- **~1,900 keyword hits** for "password" concentrated in user profile
- Cain & Abel present for live credential sniffing

### 5. Anti-Forensic Behavior
- **7,145 deleted files** on the volume
- Anonymizer software accessed (`D:\Drivers\Anonymizer`)
- GhostWare artifacts present
- Deleted executables suggest attempted evidence removal

---

## 🟡 Supporting Evidence

### File System Anomalies
- Hidden folder in user profile — not linked to any standard Windows application
- Multiple `Temp/` files created/modified in a **90-minute burst**

### Recent Documents Artifacts
- Shortcut to `D:\Drivers\Anonymizer`
- Shortcut to captured receipt data
- GhostWare shortcuts (~20 August 2004)

### Timeline Observations
- OS installed 19 August 2004
- All suspicious tool installation/use occurred within the 8-day window
- Heavy activity in `My Documents` folder throughout
- Last shutdown: 27 August 2004

---

## 📍 Evidence Locations

| Evidence | Location on Disk |
|----------|-----------------|
| John the Ripper source | `C:\Documents and Settings\Mr. Evil\My Documents\` |
| Anonymizer shortcut | `D:\Drivers\Anonymizer` (Recent Docs) |
| Captured HTTP traffic | Present in interception file |
| Deleted trojans | Unallocated space (recovered via PhotoRec) |
| Browser history (WinPcap) | IE history — `athlead.com` + others |

---

## ✅ Conclusion

All evidence points to the device being **deliberately configured as a wireless interception platform**. The 8-day activity window, rapid tool installation, active use of packet sniffers, password crackers, and the presence of captured traffic leave no ambiguity about intent. All activity is attributable to the `Mr. Evil` account.
