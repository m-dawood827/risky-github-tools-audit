# hackirby/skuld - CRITICAL

**471 stars** | Go | Self-described "PoC, educational purposes only"

## Verdict

Ye PoC nahi hai. Ye deployment-ready infostealer ka poora source code hai.

## Evidence

### 1. Operator-configured exfiltration

`main.go`:

    CONFIG := map[string]interface{}{
        "webhook": "",
        "cryptos": map[string]string{ ... },
    }

`utils/requests/requests.go`:

    func Webhook(webhook string, data map[string]interface{}, files ...string)

Multipart POST with file attachments. Operator apna Discord webhook daalta hai,
phir har module chori ka data wahan bhejta hai.

### 2. Remote payload fetch - sab se ahem

`main.go` runtime par ye fetch karta hai:

    https://raw.githubusercontent.com/hackirby/discord-injection/main/injection.js

Matlab payload repo se bahar hai. Upstream author jab chahe `injection.js`
badal sakta hai. Aap ka fork ya audited copy bekaar hai - chalte waqt naya
code download hoga. Ye supply-chain risk hai.

### 3. Modules (har aik `webhook` parameter leta hai)

| Module | Behaviour |
| --- | --- |
| modules/browsers | Browser passwords, cookies, history -> webhook |
| modules/discodes | Discord token files |
| modules/discordinjection | Discord client mein JS inject - persistence |
| modules/walletsinjection | Atomic + Exodus wallets patch |
| modules/games | Gaming account data |
| modules/system | Machine/user fingerprint |
| modules/commonfiles | Document sweep and upload |

### 4. Crypto clipper

`CONFIG["cryptos"]` operator ke wallet addresses rakhta hai. Victim jab wallet
address copy kare, clipboard mein operator ka address swap ho jata hai.

## Risk to anyone who builds it

Apne hi browser, Discord, aur crypto wallets ka data leak. Windows primary
target hai lekin Go cross-compile hota hai.

## If you starred this

- Build ya run kiya hai? Foran: Discord password change + token reset,
  browser passwords rotate, crypto wallet seed phrase se naya wallet banayein
- Public fork rakhna GitHub AUP risk hai - private kar dein ya delete

## Educational value

Code **padhne** ke liye behtareen hai - modular stealer architecture,
exfil design, injection persistence. Compile karne ke liye bilkul nahi.
