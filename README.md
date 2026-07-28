# Risky GitHub Tools — Static Analysis Audits

Popular "hacking tools" with thousands of stars — that actually target their own users. This repo is a **read-only code audit** of them.

> **Tool:** [`repo-safety-checker.html`](./repo-safety-checker.html) — a self-contained
> checker. Paste in a GitHub repo link and it tells you whether the repo looks dangerous.
> No install, no dependencies — just open it in your browser and run it.

## Methodology

- All code was read through the GitHub API only. Nothing was cloned, extracted, built, or run.
- Each repo's file tree, size, and source code were reviewed manually.
- Focus areas: exfiltration endpoints, remote payload fetching, packed binaries, committed secrets, and install-time downloads.

## Findings summary

| Repo | Stars | Verdict |
| --- | --- | --- |
| hackirby/skuld | 471 | CRITICAL — confirmed infostealer with remote payload |
| Xooppp/Cypher-MINITOOL | 30 | CRITICAL — 24MB packed binary, zero source code |
| fulluhq/BlueMagic-Multitool | 112 | HIGH — empty repo, README only, external download |
| hackerxphantom/HACK-CAMERA | 978 | MEDIUM — camera phishing kit, no exploit |
| m4lal0/backdoorPhish | 80 | MEDIUM — dual-use, clean code |
| maxi-schaefer/Chronos-Nuker | 75 | MEDIUM — abuse tool, clean code |
| dropalways/netcry-nuker | 28 | MEDIUM — abuse tool, committed token.txt |

Full details: [`audits/`](./audits)

## Why this exists

I reviewed 260 starred repos. Seven of them showed patterns that are dangerous for new learners. This repo is for the people who'll find these tools through a Google search — so they know before they hit run.

## Key red flags to look for (in any repo)

1. **Packed binary, no source** — a `.rar` / `.zip` / `.exe` with no code behind it
2. **README-only repo** — the actual file lives on an external host (MediaFire, Mega, Telegram)
3. **Remote payload fetch** — the script pulls code from somewhere like `raw.githubusercontent.com` at runtime
4. **Committed secrets** — `token.txt`, `.env`, hardcoded webhooks
5. **Self-update files** — `version.txt` plus update logic, meaning the code can change after install
6. **Install scripts** — anything that downloads something and pipes it straight into a shell
7. **Hardcoded exfiltration** — a Discord webhook, Telegram bot token, or pastebin URL baked into the code

## Green flags

- Readable source, organized in `src/` or clear modules
- A license file is present
- Launcher-only start scripts (no install-time downloads)
- No hardcoded network destinations
- Commit history that built up gradually, with multiple contributors

## If you've already run one of these

From a separate, clean device, in this order:

1. Disconnect the affected machine from the network
2. Change your Discord password, log out of all sessions, and generate new 2FA backup codes
3. Rotate every password saved in your browser — email, banking, and GitHub first
4. Revoke OAuth apps and active sessions on Google, GitHub, and Discord
5. Regenerate API keys and personal access tokens
6. **Crypto: create a new wallet with a new seed phrase and move your funds over**
7. Turn on antivirus and run a full scan
8. Check startup entries and scheduled tasks
9. Safest option: back up documents only (no executables), then reinstall the OS

## Minimal safe lab

1. Use a throwaway VM (VirtualBox / VMware / Hyper-V)
2. **Snapshot before every run** — an infection becomes a 30-second revert
3. Keep networking host-only, or off entirely
4. No shared folders, clipboard sharing, or drag-and-drop
5. No real accounts inside the VM — no Discord, no browser sync, no wallet, no SSH key
6. Revert the snapshot when you're done

## Disclaimer

This repo contains no malicious code — only analysis and documentation. Everything here is for defensive/educational purposes. Running any of these tools is not recommended. Findings reflect the code as it stood at review time, and upstream repos can change.

Running any tool on someone else's system without their written permission is a crime in most countries — including under Pakistan's PECA 2016.

---
Audited by [@m-dawood827](https://github.com/m-dawood827)
