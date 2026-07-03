# HackerOne Bug Bounty Reconnaissance

**Target:** HackerOne's own bug bounty program (HackerOne handle: \`security\`)

**Date:** 2026-07-02

## Scope

33 in-scope assets including hackerone.com, user-content CDNs, PullRequest, hacker101 CTF, and Hacker0x01 GitHub org.

## Findings

| Finding | Severity |
|---------|----------|
| mta-sts.wearehackerone.com — Wildcard CORS (GitHub Pages 404) | Informational |
| www.hackeronestatus.com — Wildcard CORS (Statuspage) | Informational |

## Structure

```
hackerone-bounty-recon/
├── README.md
└── 2026-07-02/
    ├── session-log.md
    ├── targets.txt
    ├── subdomains-all.txt
    ├── live-hosts.txt
    ├── scan-results.txt
    ├── cors-tests.txt
    └── exposed-files.txt
```
