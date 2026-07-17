# CASE-XXX — [Descriptive Incident Title]

> **Sanitization notice:** This report is based on a real incident I handled. Organization names, hostnames, usernames, IP addresses, and any identifying indicators have been removed or generalized. The analysis, decisions, and timeline are unaltered.

| Field | Value |
|---|---|
| **Case ID** | CASE-XXX |
| **Severity** | SEV-X (define your scale: SEV-1 critical → SEV-4 low) |
| **Status** | Contained / Remediated / Closed |
| **Incident type** | e.g., Credential compromise, Malware, Policy violation |
| **Detection source** | e.g., EDR alert, SIEM correlation, user report, threat hunt |
| **Dwell time** | Time from initial activity to detection |
| **Time to contain** | Time from detection to containment |
| **ATT&CK techniques** | T####, T####.### |
| **Role in response** | e.g., Lead responder, triage analyst, supporting analyst |

---

## 1. Executive Summary

*3–5 sentences, written for a non-technical reader. What happened, how it was found, what the impact was (or wasn't), and the outcome. This is the section a hiring manager reads first — make it count.*

---

## 2. Detection

*How did this activity first surface?*

- The alert, report, or hunt hypothesis that started it
- What the initial signal actually said (paraphrase the alert logic — don't paste proprietary rule content)
- Initial assessment: why this warranted escalation instead of dismissal

**Telemetry involved:** e.g., Windows Security logs (4624/4625), Sysmon Event ID 1, M365 Unified Audit Log, EDR process tree

---

## 3. Triage & Scoping

*The investigative work. This section carries the most weight with technical reviewers.*

- **Scoping questions asked:** How many hosts/accounts? Earliest evidence of activity? Any lateral movement?
- **Queries and pivots used:** Describe the logic (e.g., "pivoted from the alerting host to all authentications by the affected account in the prior 72 hours"). Sanitized query snippets are excellent here.
- **Evidence preserved:** What was collected and how (memory, disk, logs, mailbox export)
- **Severity decision:** Why this landed at the severity it did

### Key findings

| # | Finding | Evidence source |
|---|---|---|
| 1 | | |
| 2 | | |

---

## 4. Containment

*What was done to stop active harm, and in what order.*

- Actions taken (host isolation, session revocation, credential resets, rule/IOC blocks)
- **Decision rationale:** Why these actions, in this order — e.g., why you revoked sessions before resetting the password
- Anything deliberately *not* done yet, and why (e.g., preserving attacker access for scoping)

---

## 5. Remediation & Recovery

- Eradication steps (persistence removal, malicious rule cleanup, rebuild vs. clean decisions)
- Recovery and validation — how you confirmed the environment was clean
- Hardening applied to close the original entry vector

---

## 6. Lessons Learned

*The section that separates practitioners from tutorial-followers. Be honest about what was slow or missing.*

- **What worked:** Detections, playbook steps, or tooling that performed well
- **What didn't:** Gaps in visibility, delays in triage, missing playbook steps
- **What changed as a result:**
  - New/tuned detections shipped (link to the Sigma rule on GitHub if published)
  - Playbook or process updates
  - Control or configuration changes

---

## 7. MITRE ATT&CK Mapping

| Tactic | Technique | ID | Observed via |
|---|---|---|---|
| Initial Access | Phishing | T1566 | |
| Persistence | Scheduled Task/Job | T1053.005 | |

---

## 8. Timeline (Sanitized)

*Relative timestamps (T+0h) work well and avoid dating the incident.*

| Time | Event |
|---|---|
| T+0h | Earliest observed attacker activity |
| T+Xh | Detection |
| T+Xh | Triage began; severity assigned |
| T+Xh | Containment actions executed |
| T+Xh | Remediation complete |
| T+Xd | Lessons-learned review held |

---

## Appendix A — Sanitization Checklist

Confirm every item before publishing:

- [ ] Organization name, industry-identifying details, and internal team names removed
- [ ] Hostnames, domain names, and internal naming conventions generalized (e.g., `WKSTN-01`)
- [ ] Usernames and email addresses replaced with role labels (e.g., `finance-user-1`)
- [ ] Real IPs replaced with RFC 5737 documentation ranges (`192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`)
- [ ] Real file hashes removed or replaced with placeholders unless already public IOCs
- [ ] Proprietary detection content (vendor rule logic, internal playbooks) paraphrased, not pasted
- [ ] Absolute dates removed or replaced with relative timestamps
- [ ] Screenshots scrubbed of hostnames, usernames, tenant IDs, and browser tabs
- [ ] Reviewed against your employer's confidentiality/NDA obligations

---

*Report author: Adedayo · [GitHub](https://github.com/YOUR-USERNAME) · [LinkedIn](https://www.linkedin.com/in/YOUR-PROFILE)*
