# Discord Nukers - Comparative Audit

Do similar tools, bohot different code quality. Ye comparison hi audit skill
sikhata hai: **structure hi risk bata deta hai, code padhne se pehle.**

## dropalways/netcry-nuker - 28 stars | Python

| Path | Note |
| --- | --- |
| main.py | 13,047 bytes |
| commands/ | Har destructive command alag file |
| requirements.txt | 49 bytes - readable |
| setup.bat / setup.sh | Install scripts - **read before running** |
| start.bat / start.sh | Launchers |
| **token.txt (17 bytes)** | Committed to repo |
| version.txt | 3 bytes - possible self-update |

**Concerns:**

- `token.txt` repo mein commit hai. 17 bytes se lagta hai placeholder hai
  (real Discord bot token ~59-72 chars), lekin agar author ne kabhi asal token
  commit kiya to git history mein ab bhi hoga - aur har fork mein copy ho chuka.
- `setup.sh` install ke waqt kuch download kar sakta hai
- `version.txt` self-update mechanism ki nishani - code runtime par badal sakta hai

## maxi-schaefer/Chronos-Nuker - 75 stars | Python

| Path | Note |
| --- | --- |
| src/ | Proper package layout |
| requirements.txt | 58 bytes |
| start.bat | 122 bytes - launcher only |
| LICENSE | MIT |

**Cleaner:** koi committed token nahi, koi install-time download script nahi,
koi self-update nahi, proper `src/` layout, license maujood.

## Side by side

| | Chronos-Nuker | netcry-nuker |
| --- | --- | --- |
| Structure | src/ package | root par bikhra |
| Committed secrets | none | token.txt |
| Install script | launcher only | setup.sh + setup.bat |
| Self-update | no | version.txt |
| License | MIT | none |

## Both tools

Khatra tool ke andar chhupa hua nahi hai - tool ke **maqsad** mein hai.
Kisi server par chalana Discord ToS violation hai (permanent ban), aur
doosre ke server par chalana bohot mulkon mein criminal offence hai
(Pakistan: PECA 2016).

## Defensive value

`commands/` padh kar samajh aata hai ke Discord bot permissions ka misuse
kaise hota hai - aur apne server par audit log monitoring, role hierarchy,
aur bot permission scoping kaise theek karein.
