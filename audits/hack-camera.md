# hackerxphantom/HACK-CAMERA - MEDIUM

**978 stars** | Bash + PHP

## Verdict

Camera-grabbing phishing kit. Naam misleading hai - koi "hack" nahi, koi
exploit nahi. Purely social engineering.

## Evidence

| Path | Note |
| --- | --- |
| hack_camera.sh | 16,306 bytes - main orchestrator |
| IP.php | 517 bytes - victim IP logging |
| setup | 1,766 bytes - dependency installer, read before running |
| fest/ jio/ om/ live/ | Fake page templates |
| files/ | Assets |

## How it works

1. Fake webpage host karta hai (Jio offer, festival greeting, live stream)
2. Page browser ka `getUserMedia()` call karta hai - camera permission maangta hai
3. Victim "Allow" kare to snapshots capture aur upload
4. `IP.php` IP log karta hai
5. Tunneling service se local server ko public link milta hai

**Browser permission ke baghair kaam nahi karta.** Koi vulnerability exploit
nahi hoti - sirf victim ka "Allow" dabana.

## Notes

- Repo mein khud koi stealer signal nahi mila - koi packed binary, koi
  hardcoded webhook nahi
- Lekin `setup` script dependencies install karta hai - chalane se pehle padhein
- `fest/` `jio/` `om/` templates batate hain ke kit South Asian users ke liye
  tuned hai

## Defensive takeaway

Sab se qeemti lesson: **kitna aasan hai** aisa page banana. Isi liye:

- Unknown links par camera/mic permission na dein
- Browser mein camera "Ask every time" par rakhein
- Non-technical family ko ye demo dikhayein - awareness ke liye best example
