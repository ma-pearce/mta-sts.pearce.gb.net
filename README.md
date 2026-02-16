# 🔒 MTA-STS Policy for pearce.gb.net

This repository hosts the [MTA-STS](https://datatracker.ietf.org/doc/html/rfc8461) (Mail Transfer Agent Strict Transport Security) policy for **pearce.gb.net**, served via [GitHub Pages](https://pages.github.com/).

## 📋 What is MTA-STS?

MTA-STS is an email security standard that enables mail servers to declare their ability to receive TLS-secured connections. It prevents TLS downgrade attacks and man-in-the-middle interception of email traffic by instructing sending mail servers to:

- Only deliver mail over encrypted (TLS) connections
- Validate the receiving server's certificate
- Refuse delivery if a secure connection cannot be established

## 🌐 How It Works

1. A sending mail server looks up the `_mta-sts.pearce.gb.net` TXT record to discover that this domain supports MTA-STS
2. It fetches the policy file from `https://mta-sts.pearce.gb.net/.well-known/mta-sts.txt`
3. The policy specifies which MX servers are valid and that TLS is enforced
4. The sending server caches the policy and enforces it for the duration of `max_age`

## 📁 Repository Structure

```
├── .well-known/
│   └── mta-sts.txt    # MTA-STS policy file
├── .nojekyll           # Ensures GitHub Pages serves .well-known directory
├── CNAME               # Custom domain configuration for GitHub Pages
├── index.html          # Minimal root page
├── LICENSE             # MIT License
└── README.md
```

## 🔧 DNS Records

The following DNS records are required alongside this repository:

| Type | Host | Value |
|------|------|-------|
| CNAME | `mta-sts` | `ma-pearce.github.io` |
| TXT | `_mta-sts` | `v=STSv1; id=20260216` |

> **Note:** The `id` field in the TXT record should be updated whenever the policy file changes, to signal to caching mail servers that a new policy is available.

## 🔗 Related Standards

- [RFC 8461 — SMTP MTA Strict Transport Security](https://datatracker.ietf.org/doc/html/rfc8461)
- [RFC 8460 — SMTP TLS Reporting (TLS-RPT)](https://datatracker.ietf.org/doc/html/rfc8460)
- [RFC 7489 — DMARC](https://datatracker.ietf.org/doc/html/rfc7489)

## 📜 License

This project is licensed under the [MIT License](LICENSE).
