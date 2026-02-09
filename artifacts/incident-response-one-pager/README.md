# Incident Response One-Pager (Small Business — First 60 Minutes)

## Purpose
Provide a practical, first-response checklist for small businesses experiencing a suspected security incident. This one-pager prioritizes containment, evidence preservation, and decision-making that reduces harm and supports follow-on investigation.

## Scope
**In scope:** first 60-minute actions, containment, evidence capture, communications, escalation triggers, and recovery stabilization.  
**Out of scope:** full digital forensics, legal advice, and enterprise-scale incident handling.

---

## 0–10 Minutes: Stabilize and Preserve
### DO
- **Start an incident log:** time, who reported it, what was observed, affected systems, actions taken.
- **Preserve evidence:** take screenshots of alerts/messages/ransom notes; record file names and paths.
- **Isolate affected device(s):** disconnect from Wi-Fi/Ethernet (do not power off unless instructed by IR lead).
- **Identify the blast radius:** what accounts, endpoints, servers, cloud apps, and business functions are impacted.

### DO NOT
- Do **not** wipe systems or “clean install” during initial response.
- Do **not** reuse the affected device to change passwords or contact attackers.
- Do **not** pay or negotiate from any potentially compromised system.
- Do **not** forward suspicious emails/attachments to coworkers (use reporting workflow).

---

## 10–30 Minutes: Contain the Incident
### Account and Access Containment
- Disable or reset credentials for **suspected compromised accounts** (prioritize admin, finance, email).
- Enforce **MFA reset** where available; revoke active sessions/tokens (cloud/email platforms).
- If “MFA fatigue” suspected, implement **number matching** or tighten MFA policy (if supported).

### Network and Endpoint Containment
- Block known malicious domains/IPs (if confirmed) on router/firewall/DNS provider.
- Quarantine suspicious email messages at the mail platform if the incident is email-based.
- If ransomware suspected: isolate additional endpoints showing encryption/IOCs; stop spread.

### Business Containment
- Freeze high-risk business processes temporarily (wire transfers, vendor payment changes, new bank details).
- Confirm critical backups are not being overwritten (pause scheduled jobs if necessary).

---

## 30–60 Minutes: Collect Key Evidence (Minimum Viable IR Package)
Capture and store these items in a secure location (admin laptop or cloud drive not involved in the incident):

### A) What happened (facts)
- Incident start time (first known) and detection time
- Symptoms observed (pop-ups, ransom note, suspicious login alerts, missing files)
- Systems/users affected (list)
- Actions already taken (list)

### B) Email and Identity Evidence (if relevant)
- Suspicious email(s): subject, sender, reply-to, time received, URL(s) (defanged)
- User action: clicked link? opened attachment? entered credentials? approved MFA prompt?
- Authentication evidence (from admin console): unusual logins, impossible travel, new devices

### C) Host and Network Evidence (if relevant)
- Hostname, OS, IP address (internal), logged-in user
- Suspicious filenames/paths; hashes if available
- Security tool alerts (AV/EDR/Defender) screenshots
- Router/firewall logs or connection summaries (as available)

### D) IOCs (Indicators of Compromise)
- Domains/URLs (defanged), IPs, file hashes, sender addresses
- Keep a simple tracking table (IOC, source, confidence, action taken)

---

## Escalation Triggers (When to Call for Help)
Escalate immediately if any of the following are true:
- Suspected ransomware, widespread encryption, or data exfiltration indicators
- Compromise of admin accounts, email tenant admin, or financial accounts
- Confirmed credential submission to a suspicious site
- Customer/employee data may be exposed (privacy/regulatory implications)
- Incident is ongoing and containment is uncertain

**Who to contact (typical):**
- Managed IT/MSSP or IR vendor (preferred)
- Cyber insurance provider (if coverage exists)
- Legal counsel (if data exposure suspected)
- Law enforcement (case-dependent; follow counsel/insurer guidance)

---

## Communications (Keep it Controlled)
- Assign a single incident coordinator/point of contact.
- Keep updates factual; avoid speculation.
- Do not discuss incident details in compromised channels (use alternate comms if needed).
- Document deci

