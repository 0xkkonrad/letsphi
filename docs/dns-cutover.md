# DNS cut-over: Google Sites → GitHub Pages

Status as of 2026-07-12: site deployed to GitHub Pages, previewing at
<https://kkonrad.com/letsphi/>. Custom domain **not yet attached** — do that
after the DNS change below.

## Current state

| Record | Value | Meaning |
|---|---|---|
| Registrar | Squarespace Domains II LLC | ex-Google Domains, migrated 2023/24 |
| NS | ns-cloud-c1…c4.googledomains.com | DNS managed via Squarespace panel |
| A (apex) | 198.49.23.144 | Squarespace parking, 301 → www |
| CNAME www | ghs.googlehosted.com | the old Google Sites site |
| MX | mxa/mxb.mailgun.org | **email — do not touch** |
| TXT | `v=spf1 include:mailgun.org ~all` | **email — do not touch** |

## Steps (in the Squarespace DNS panel)

Log in at <https://account.squarespace.com> → **Domains** → `letsphi.com` →
**DNS** / Edit DNS. (Login is most likely "Continue with Google" with the
account that originally held the domain at Google Domains.)

1. **Delete** the apex `A` record `198.49.23.144` (and any sibling
   `198.185.159.x` records or apex→www forwarding rule).
2. **Add** four apex `A` records (host `@`), all TTL default:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
3. Optional but recommended — add four apex `AAAA` records:
   - `2606:50c0:8000::153`
   - `2606:50c0:8001::153`
   - `2606:50c0:8002::153`
   - `2606:50c0:8003::153`
4. **Change** the `www` CNAME from `ghs.googlehosted.com` →
   `0xkkonrad.github.io.`
5. **Leave the MX and TXT (Mailgun) records exactly as they are.**

## After the DNS change

Attach the domain to the Pages site (either in repo Settings → Pages →
Custom domain, or):

```bash
gh api repos/0xkkonrad/letsphi/pages -X PUT -f cname=letsphi.com
```

GitHub then provisions a Let's Encrypt certificate (minutes up to ~1 h).
Once the cert is issued, enforce HTTPS:

```bash
gh api repos/0xkkonrad/letsphi/pages -X PUT -F https_enforced=true
```

`www.letsphi.com` will redirect to the apex automatically once both records
resolve.

Optional hardening: verify the domain for the GitHub account
(github.com → Settings → Pages → Verified domains → `letsphi.com`) so nobody
can claim it if the Pages site is ever deleted.

## Rollback

The old Google Sites site stays intact at Google Sites — restoring the old
`www` CNAME (`ghs.googlehosted.com`) and apex A (`198.49.23.144`) reverts
everything.
