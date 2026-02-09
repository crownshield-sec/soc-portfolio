# Phishing Spotter Guide (SOC L1 Triage Cards)

## Purpose
Provide a practical, repeatable method for identifying phishing and social engineering emails using common indicators, lightweight header checks, and safe handling guidance. This guide is written to support SOC Level 1 triage and end-user reporting.

## Scope
**In scope:** initial phishing identification, triage indicators, basic header review (high-level), safe URL handling, and recommended containment actions.  
**Out of scope:** malware detonation, deep reverse engineering, and enterprise-wide remediation at scale.

---

## SOC L1 Triage Flow (60–90 seconds)
1. **Pause and preserve:** Do not click links or open attachments. Capture screenshots if needed.
2. **Check the sender:** Display name vs actual address; reply-to mismatch; lookalike domains.
3. **Check the ask:** Credentials, MFA approvals, gift cards, payment changes, urgency, secrecy.
4. **Check links safely:** Hover to preview; compare domain to the claimed brand; defang URLs.
5. **Check attachments:** Unexpected attachments; macro-enabled Office files; password-protected archives.
6. **Decide & route:**
   - **Likely phishing:** quarantine/delete, report, block IOCs as appropriate.
   - **Unclear:** verify through a trusted channel (known phone number/internal directory), then decide.

---

## High-Signal Indicators (What to Look For)

### A) Sender and Identity Indicators
- Display name does not match email domain (e.g., “Microsoft Support” from a random domain)
- Lookalike domains (e.g., `micros0ft.com`, `rnicrosoft.com`, extra hyphens)
- Reply-To differs from From address
- Unexpected external sender for internal-only workflows

### B) Content and Social Engineering Indicators
- Urgency/threat language: “account will be locked,” “final notice,” “action required”
- Unusual secrecy or pressure to bypass normal process
- Requests for credentials, MFA approvals, one-time codes, or password resets
- Payment/invoice changes or bank account updates (BEC pattern)
- “Too good to be true” offers or unexpected refunds

### C) Link and Destination Indicators (Safe Handling)
- Hovered link domain differs from the brand claimed in the email
- Link uses URL shorteners or unusual subdomains
- Link points to an IP address or suspicious TLD
- Domain is newly registered or unrelated to the sender’s organization (verify if possible)

### D) Attachment Indicators
- Macro-enabled files: `.docm`, `.xlsm`
- Archives: `.zip`, `.rar`, `.7z`, especially if password-protected
- Executables disguised as documents (double extensions: `invoice.pdf.exe`)
- Unusual file delivery for that business process (e.g., “HR policy update” as a zip file)

---

## Lightweight Header Checks (SOC L1 Level)
You do not need deep email forensics for initial triage, but these checks often help:

- **SPF/DKIM/DMARC results:** failures or “none” can be suspicious (not definitive alone)
- **Return-Path vs From mismatch:** can indicate spoofing or third-party senders
- **Received path anomalies:** unexpected mail servers or regions (context matters)

> Note: Legitimate marketing or ticketing systems can also cause mismatches. Treat headers as supporting evidence, not the only evidence.

---

## Triage Cards (Realistic Examples — Sanitized)

### Card 1 — Credential Harvest (Fake Password Expiration)
**Subject:** “Password Expiring Today — Action Required”  
**Claimed Sender:** “IT Support”  
**Observed Indicators:**
- Urgency + threat of lockout
- Generic greeting (“Dear User”)
- Hover link points to non-corporate domain
- Reply-To differs from From
**Risk:** Credential theft leading to account takeover  
**SOC L1 Action:**
- Treat as phishing; report to security mailbox/queue
- Defang and capture the URL as an IOC
- If clicked/entered creds: initiate password reset + session revocation (per org process)

**IOC Examples (defanged):**
- `hxxps://login-confirmation[.]example-support[.]com`

---

### Card 2 — Business Email Compromise (Invoice / Payment Change)
**Subject:** “Updated Banking Details for Invoice #48219”  
**Claimed Sender:** “Vendor Accounts”  
**Observed Indicators:**
- Request to change payment destination
- Pressure to “process today”
- Sender domain is close but not exact (lookalike)
- Attachment included to “confirm banking info”
**Risk:** Fraudulent wire transfer / financial loss  
**SOC L1 Action:**
- Flag as likely BEC; escalate to finance/AP + security lead
- Verify vendor request via trusted contact method (known phone number)
- Preserve the email for investigation; capture sender + domains as observables

---

### Card 3 — Malware Delivery (Trojanized Document)
**Subject:** “Shipment Label / Delivery Notice”  
**Observed Indicators:**
- Unexpected attachment with macros (`.docm`) or archive (`.zip`)
- Language errors + urgency (“delivery failed”)
- Brand mismatch (FedEx/UPS claim but non-brand sender domain)
**Risk:** Malware infection → persistence → lateral movement  
**SOC L1 Action:**
- Quarantine and block attachment hash (if available)
- If opened: isolate host, collect initial triage details (user, time, filename), escalate
- Capture sender domain + file name + any URLs as observables

---

## Reporting Template (Copy/Paste)
Use this when reporting suspected phishing:

- **Time received:**  
- **Sender (display name + email):**  
- **Subject:**  
- **User action taken:** (clicked link? opened attachment? entered credentials?)  
- **Indicators observed:** (sender mismatch, urgency, link mismatch, attachment type)  
- **IOCs captured (defanged):** (URLs/domains/hashes if available)  
- **Recommended action:** (quarantine, block, password reset, isolate host, escalate)

---

## Data Handling Note
All examples are sanitized. Identifiers (domains, IPs, usernames, hostnames, timestamps) are redacted or replaced with representative values. No proprietary or sensitive customer/employer data is included.

