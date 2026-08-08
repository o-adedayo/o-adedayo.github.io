# o-adedayo.github.io

Portfolio site for **Adedayo** — IT professional working across Help Desk and Incident
Response, moving toward a SOC Analyst role.

**Live site:** [o-adedayo.github.io](https://o-adedayo.github.io)

## What's here

This repo is the source for a single-page portfolio plus two sanitized write-up
collections, all styled to match:

| Path | Contents |
|---|---|
| `index.html` | The portfolio landing page — IR case study cards, a detection engineering section (Sigma rules), home lab research, and IT Support & Troubleshooting |
| `case-studies/` | Sanitized incident response case studies (`CASE-XXX`) — detection through lessons learned, mapped to MITRE ATT&CK |
| `support-cases/` | Sanitized IT Help Desk troubleshooting write-ups (`TKT-XXX`) — symptom through root cause and fix |

Every case study and support write-up has a matching `template.html` in its folder,
so new entries stay visually and structurally consistent.

> **Note on sanitization:** All write-ups are based on real incidents and tickets I've
> worked. Organization names, hostnames, usernames, IP addresses, and other identifying
> details are removed or generalized (RFC 5737 documentation IPs where an address is
> needed) before publishing.

## Why IT Support is included

Help desk work is the first line of detection — the tier where a routine ticket either
gets closed or escalated into a real incident. It's included here deliberately, as
evidence of the same triage instincts and endpoint fluency that carry into IR work, not
as a separate or lesser track.

## Stack

Plain HTML/CSS, no build step — everything is edited directly in the GitHub web editor
and served via GitHub Pages from the `main` branch.

## Contact

[GitHub](https://github.com/o-adedayo) · [LinkedIn](https://www.linkedin.com/in/adedayoogungbemi/) · [Email](ogungbemiadedayo@gmail.com)
