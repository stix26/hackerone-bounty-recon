# Bug Bounty Session — 2026-07-02 (HackerOne)

**Target:** HackerOne's own bug bounty program (handle: `security`, id: 13)
**HackerOne User:** stix26
**Date:** 2026-07-02

---

## Summary

Full recon against HackerOne's own bounty program. Discovered via H1 API program listing. 33 in-scope assets identified including `hackerone.com`, user-content domains, PullRequest (acquisition), hacker101.com CTF, and the Hacker0x01 GitHub org.

**No exploitable vulnerabilities found.** Two misconfigurations noted.

## Scope Coverage

- **hackerone.com** — main site, API, docs, support — verified accessible
- ***.hackerone-user-content.com** — user content CDN — 404 on most paths
- ***.hackerone-ext-content.com** — ext content CDN — a5s/b5s return 200
- **errors.hackerone.net** — error tracking — DNS flaky, no response
- **hackerone.live** — redirects to hackerone.com via Cloudflare
- **app.pullrequest.com / reviewer.pullrequest.com** — PullRequest acquisition
- **ctf.hacker101.com** — CTF platform — accessible
- **mta-sts.wearehackerone.com** — GitHub Pages hosted, 404 with wildcard CORS
- **www.hackeronestatus.com** — Atlassian Statuspage with wildcard CORS
- **github.com/Hacker0x01/react-datepicker** — in scope (no bounty)

## Notable Findings

### 1. mta-sts.wearehackerone.com — Wildcard CORS
- Returns `Access-Control-Allow-Origin: *`
- Served via **GitHub Pages** (server: GitHub.com)
- Returns 404 "File not found" (no content to exfiltrate)
- **Severity:** Informational — misconfiguration, but no security impact

### 2. www.hackeronestatus.com — Wildcard CORS
- Returns `Access-Control-Allow-Origin: *`
- Powered by Atlassian Statuspage (public status page)
- Status pages are public by design
- **Severity:** Informational

## Pipeline Results

| Step | Result |
|------|--------|
| H1 API program discovery | Found 33 scopes for HackerOne program |
| Subdomain enumeration | 104 unique subdomains across 6 related domains |
| Live host probing | 19 live hosts identified |
| CORS testing | 2 wildcard CORS found (low severity) |
| Exposed file scanning | No exposed files found |
| GitHub commit analysis | No security-relevant commits found |

## Repos Created

- `github.com/stix26/hackerone-bounty-recon` — Full recon results
