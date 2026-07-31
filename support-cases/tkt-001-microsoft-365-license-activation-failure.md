# TKT-001 — Microsoft 365 "License Activation Failure (Errors Persisting After Reinstall)

> **Sanitization notice:** Based on a real support case. User names, hostnames, and organization-identifying details have been removed or generalized.

| Field | Value |
|---|---|
| **Ticket ID** | TKT-001 |
| **Category** | Endpoint / Identity |
| **Priority** | P3 |
| **Environment** | Windows, Microsoft 365 Business Premium, Entra ID-managed tenant |
| **Time to resolve** | Multi-session (initial triage, reinstall attempt, follow-up remediation) |
| **Outcome** | Resolved |

---

## 1. Reported Symptom

*"Word and Outlook say I'm not licensed and most of my features are greyed out."*

Translated: the user was seeing full-screen "Sign in to get started with Outlook" activation prompts, an "Outlook (Unlicensed Product)" title bar, and Word banners reading "stored credentials are out of date" and "most features are disabled because your Office product is inactive." This pattern points to a license *validation* failure on the client, not necessarily a missing license — those are two different problems that look identical to the end user.

## 2. Initial Hypotheses

1. The user's M365 license was never assigned or had lapsed (tenant-side).
2. The license was assigned but failed to provision correctly against one or more services (partial provisioning error).
3. The license was fine, but the local Office installation was corrupted or never activated on this device (client-side).
4. The license was fine, but stale cached credentials/tokens on the endpoint were blocking Office from validating it, even after a clean reinstall.

## 3. Diagnostic Path

| Step | Check | Tool / Command | Result | Ruled out / Confirmed |
|---|---|---|---|---|
| 1 | Confirmed license assignment | M365 Admin Center → Active Users → Licenses | Microsoft 365 Business Premium and Entra ID P2 both shown as assigned | Ruled out: missing license |
| 2 | Confirmed per-service provisioning state | Entra ID admin center → user → Licenses blade | Business Premium 53/53 services enabled; Entra ID P2 4/4 enabled; both Direct assignment, State: Active | Ruled out: partial/failed provisioning |
| 3 | Attempted full reinstall of Office | Uninstall/reinstall Microsoft 365 Apps on endpoint | Unlicensed banners reappeared after sign-in | Ruled out: corrupted installation |
| 4 | Reviewed what a reinstall actually clears | Manual review of Office uninstall behavior | Confirmed reinstall does not clear Windows Credential Manager entries or Office's local token cache folder | Confirmed: stale cached credentials as likely cause |
| 5 | Cleared Windows Credential Manager entries | Control Panel → Credential Manager → Windows Credentials | Removed stale Microsoft/Office-related entries | Remediation step |
| 6 | Signed out of Windows-level Microsoft account | Settings → Accounts → Email & accounts | Removed cached identity session outside of Office itself | Remediation step |
| 7 | Cleared Office's local token cache folder | Local token cache folder | Cleared cached identity/session tokens | Remediation step |
| 8 | Rebooted and re-authenticated | Reboot → sign in to Word with user's UPN | License activated successfully; features restored | Confirmed fix |

## 4. Root Cause

The license itself was fully active and correctly provisioned at the tenant level — this was verified directly in Entra ID before any client-side changes were made, which kept the investigation from wasting time on the wrong layer. The actual problem was stale cached Microsoft identity/session data on the endpoint (Windows Credential Manager entries, a linked Windows-level Microsoft account session, and Office's local token cache) that was preventing Office from successfully validating the license against the current session. A standard Office uninstall/reinstall does not touch any of these locations, which is why the first remediation attempt didn't resolve it — the corrupted-install hypothesis looked right until the reinstall failed to fix it, at which point the cache hypothesis became the stronger explanation.

## 5. Fix Applied

Cleared the stale Windows Credential Manager entries, signed out of the Windows-level Microsoft account linked to the device, and cleared Office's local token cache folder. Rebooted the endpoint and signed back into Word with the user's correct M365 credentials. Verified resolution by confirming the unlicensed/inactive banners no longer appeared and that full Office editing functionality (not just the absence of complaints) was restored and remained stable after reopening the applications.

## 6. Prevention / Follow-Up

Documented internally that "Unlicensed Product" symptoms surviving a clean Office reinstall should prompt clearing Windows Credential Manager entries, the linked Windows-level Microsoft account, and Office's local token cache as a standard next step rather than repeating the reinstall or escalating prematurely. This sequencing (verify tenant-side license health first, then work through client-side identity cache layers) is being carried forward as the default triage order for similar activation tickets going forward.

## Skills Demonstrated

`Microsoft Entra ID` · `M365 Admin Center` · `License/service-plan auditing` · `Windows Credential Manager` · `Layered elimination (tenant vs. client isolation)` · `Root cause analysis distinguishing tenant-level faults from endpoint-level faults` · `Structured, evidence-based troubleshooting methodology (backend-first verification before client-side changes)`


## Security Note (if applicable)

No security dimension identified. Verified early in triage that this was a license validation/identity cache issue rather than an account compromise indicator — no unusual sign-in activity, no unauthorized license or permission changes, and no account security posture changes were made or required.

---

*Author: Adedayo · [Portfolio](https://o-adedayo.github.io) · [GitHub](https://github.com/o-adedayo)*
