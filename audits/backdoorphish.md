# m4lal0/backdoorPhish - MEDIUM

**80 stars** | Bash + PHP | Spanish-language project

## Verdict

Phishing page + reverse-shell payload generator. Genuine dual-use tool -
real pentest value, lekin misuse bhi aasan. Code saaf hai.

## Evidence

| Path | Note |
| --- | --- |
| backdoorPhish.sh | 19,157 bytes - single script, sab kuch yahan |
| get_ip.php | 551 bytes - victim IP capture |
| info.php | 1,176 bytes - browser/device fingerprint |
| templates/ | Fake login pages |

## How it works

1. **Phishing side** - `templates/` se fake page host, `get_ip.php` +
   `info.php` victim ka IP aur device info log karte hain
2. **Payload side** - Windows/Android reverse-shell backdoor generate karta hai
   (msfvenom wrap), Ngrok se tunnel bana kar listener public

## Positive signals

- Koi hardcoded exfil endpoint nahi mila - koi Discord webhook, koi Telegram
  bot token, koi packed binary nahi. Tool apne user ko target nahi karta.
- 19 KB single bash script - fully auditable

## Cautions

- Ngrok authtoken script mein jata hai - throwaway account use karein
- Script dependencies install karta hai (metasploit, php, curl)

## Educational value

Is list ka sab se instructive tool. Aik hi jagah poora attack chain: lure page,
victim fingerprinting, payload delivery, C2 tunnel. Bash mein hai to har step
readable - koi magic nahi. Isi se samajh aata hai ke email attachment scanning,
EDR, aur outbound tunnel detection kyun zaroori hain.
