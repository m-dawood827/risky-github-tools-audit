# Risky GitHub Tools - Static Analysis Audits

Popular "hacking tools" jinke paas hazaron stars hain, lekin jo apne users ko hi
target karte hain. Ye repo un ka **read-only code audit** hai.

> **Tool:** [`repo-safety-checker.html`](./repo-safety-checker.html) - aik self-contained
> checker. GitHub repo ka link paste karein, ye batayega ke repo khatarnak hai ya nahi.
> Koi install nahi, koi dependency nahi - browser mein kholein aur chalayein.

## Methodology

- Sirf GitHub API se code padha gaya. Kuch clone, extract, build, ya run nahi kiya.
- Har repo ka file tree, size, aur source code manually review kiya gaya.
- Focus: exfiltration endpoints, remote payload fetching, packed binaries,
  committed secrets, aur install-time downloads.

## Findings summary

| Repo | Stars | Verdict |
| --- | --- | --- |
| hackirby/skuld | 471 | CRITICAL - confirmed infostealer with remote payload |
| Xooppp/Cypher-MINITOOL | 30 | CRITICAL - 24MB packed binary, zero source code |
| fulluhq/BlueMagic-Multitool | 112 | HIGH - empty repo, README only, external download |
| hackerxphantom/HACK-CAMERA | 978 | MEDIUM - camera phishing kit, no exploit |
| m4lal0/backdoorPhish | 80 | MEDIUM - dual-use, clean code |
| maxi-schaefer/Chronos-Nuker | 75 | MEDIUM - abuse tool, clean code |
| dropalways/netcry-nuker | 28 | MEDIUM - abuse tool, committed token.txt |

Details: [`audits/`](./audits)

## Why this exists

Main ne 260 starred repos ka review kiya. In 7 mein aise patterns mile jo
naye learners ke liye khatarnak hain. Ye repo un logon ke liye hai jo in tools
ko Google kar ke aayenge - taake wo run karne se pehle jaan lein.

## Key red flags to look for (kisi bhi repo mein)

1. **Packed binary, no source** - `.rar` / `.zip` / `.exe` bina code ke
2. **README-only repo** - asal file kisi external host par (MediaFire, Mega, Telegram)
3. **Remote payload fetch** - runtime par `raw.githubusercontent.com` se script download
4. **Committed secrets** - `token.txt`, `.env`, hardcoded webhooks
5. **Self-update files** - `version.txt` + update logic = code runtime par badal sakta hai
6. **Install scripts** - jo download kar ke seedha shell mein bhej dete hain
7. **Hardcoded exfil** - Discord webhook, Telegram bot token, pastebin URL

## Green flags

- Padhne qabil source, `src/` ya clear modules mein
- License file maujood
- Launcher-only start scripts (install-time download nahi)
- Koi hardcoded network destination nahi
- Dheere dheere bani commit history, multiple contributors

## If you already ran one of these

Ek doosre saaf device se, isi tarteeb mein:

1. Affected machine ka network band karein
2. Discord password change karein, sab sessions se logout, 2FA backup codes naye banayein
3. Browser mein save sab passwords rotate karein - email, banking, GitHub pehle
4. Google / GitHub / Discord par OAuth apps aur active sessions revoke karein
5. API keys aur personal access tokens regenerate karein
6. **Crypto: naya wallet naye seed phrase se banayein aur funds move karein**
7. Antivirus on karein aur full scan chalayein
8. Startup entries aur scheduled tasks check karein
9. Sab se safe: sirf documents backup (koi executable nahi), phir OS reinstall

## Safe lab, minimally

1. Throwaway VM (VirtualBox / VMware / Hyper-V)
2. **Har run se pehle snapshot** - infection 30 second ka revert ban jata hai
3. Network host-only ya bilkul off
4. Koi shared folder, clipboard sharing, ya drag-and-drop nahi
5. VM ke andar koi asli account nahi - na Discord, na browser sync, na wallet, na SSH key
6. Kaam ke baad snapshot revert karein

## Disclaimer

Is repo mein koi malicious code nahi hai - sirf analysis aur documentation.
Sab kuch defensive/educational maqsad ke liye hai. Koi tool run karne ki
sifarish nahi ki gayi. Findings review ke waqt ke code par mabni hain aur
upstream repos badal sakte hain.

Kisi doosre ke system par bina likhi hui ijazat koi bhi tool chalana bohot
mulkon mein jurm hai - Pakistan mein PECA 2016 ke tehat.

---
Audited by [@m-dawood827](https://github.com/m-dawood827)
