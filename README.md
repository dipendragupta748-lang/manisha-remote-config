# manisha-remote-config

Public HTTPS host for Manisha's signed remote-config / kill-switch file.

**App default URL (baked into the APK):**

```
https://raw.githubusercontent.com/dipendragupta748-lang/manisha-remote-config/main/config.json
```

## What is here now

`config.json` is an **empty signed-envelope stub**. The Manisha app will fetch it over HTTPS, then **reject** it (fail-closed) until you overwrite it with a real file signed by your private key `k1` (see `tools/sign-config/README.md` in My-manisha-agent).

Empty `payload_b64` / `sig_b64` → signature verify fails → phone keeps defaults (unlocked) or last-good signed state. That is intentional until you upload a real signed config.

## How to publish a real signed config

1. On your own computer, sign your settings with `sign_remote_config.py --legacy-mirror` (and `--prev` after the first upload).
2. Replace `config.json` in this repo with the signer output (commit + push), **or** upload the same bytes to any other HTTPS URL and point Settings → License server at it.
3. Never put private keys in this repo.

## Notes

- This repo is public on purpose: the file is meant to be world-readable; security comes from the ES256 signature, not secrecy of the JSON.
- Do not commit private keys, keystores, or unsigned production settings that you intend to treat as authoritative.
