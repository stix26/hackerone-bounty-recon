# Bug Bounty Recon: security (HackerOne)

**Date:** 2026-07-05  
**Target:** security (HackerOne) — `hackerone.com`  
**Bounty Program:** Yes — HackerOne  

## Summary

Subdomain enumeration, live probing, CORS testing, exposed file scanning, nuclei scanning, and directory fuzzing performed against the HackerOne security program.

## Results

### Subdomain Enumeration (subfinder)
Found **11 subdomains** including:
- `www.hackerone.com` (HTTP 200) — Main site
- `api.hackerone.com` (HTTP 200) — Public API
- `support.hackerone.com` (HTTP 302) — Support portal
- `docs.hackerone.com` (HTTP 302) — Documentation
- `mta-sts.hackerone.com` (HTTP 404) — MTA STS policy
- `gslink.hackerone.com` (HTTP 404)
- `websockets.hackerone.com` (HTTP 000 — WebSocket endpoint)
- `a.ns.hackerone.com` / `b.ns.hackerone.com` (HTTP 000 — Nameservers)

### CORS Testing
- `www.hackerone.com`: No `Access-Control-Allow-Origin` header returned (403 on arbitrary path test via Drupal WAF)
- `api.hackerone.com`: No CORS headers present (properly configured)
- **No misconfigurations detected**

### Exposed Files
- `hackerone.com/backup` — HTTP 200 (0 bytes — possible edge page)
- `hackerone.com/wp-admin` — HTTP 200 (0 bytes)
- `hackerone.com/sitemap.xml` — HTTP 200 (0 bytes)
- `hackerone.com/robots.txt` — HTTP 200 (0 bytes)
- `/.env`, `/.git/config`, `/dump.sql`, `/admin`, `/api`, `/config.php`, `/crossdomain.xml` — All HTTP 404 (properly restricted)

### Nuclei Scanning
- **Misconfiguration scan**: 555 templates executed — **0 findings**
- **CVE scan**: 42 templates executed — **0 findings**

### Directory Fuzzing (ffuf)
All sensitive paths return **HTTP 403** via Cloudflare/Drupal WAF:
`admin`, `api`, `.env`, `.git`, `backup`, `config`, `dashboard`, `login`, `wp-admin`, `swagger`, `graphql`, `database`, `sql`, `status`, `support`, `docs`, `health`, `metrics`, `monitor`

### Notes
- Strong security posture. Cloudflare WAF + Drupal CMS with Drupal's security layer actively blocking/filtering requests.
- No exposed sensitive files or CORS misconfigurations found.
