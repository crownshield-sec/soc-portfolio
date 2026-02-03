# Escalation Summary — Phishing Email (Lab)

## Executive Summary
A user reported a suspicious email containing an urgent call-to-action and a link to external infrastructure. Initial triage indicates likely phishing with potential for credential theft or follow-on compromise. Containment actions are recommended, with Level 2 validation required if user interaction or credential exposure is suspected.

## Timeline (Sanitized)
- T0: Email received
- T1: User reported the message / alert generated
- T2: Level 1 triage completed; indicators extracted
- T3: Containment recommendations prepared; escalation decision made

## Key Findings (Sanitized)
- Email exhibits phishing characteristics (lure/urgency, destination mismatch patterns, or authentication anomalies).
- Indicators include `<SANITIZED_DOMAIN_1>`, `<SANITIZED_DOMAIN_2>`, `<SANITIZED_URL_1>` (if observed).
- Risk depends primarily on exposure confirmation (clicked link, credential entry, attachment execution).

## Scope (Initial)
- Known affected: 1 user (<SANITIZED_USER>)
- Additional recipients: Unknown at Level 1; requires gateway search
- Credential exposure: Unknown at Level 1; requires user confirmation and identity log review

## Recommended Containment (Immediate)
- Quarantine the email and block identified domains/URLs in email security controls and web filtering.
- Search mailboxes for similar messages (campaign suppression).
- If interaction occurred: reset credentials and enforce MFA; monitor for suspicious sign-ins.

## Level 2 Requested Actions
- Confirm exposure:
  - Email security telemetry: delivery scope and click tracking (if available)
  - User confirmation: click/credential entry/attachment execution
- Identity validation:
  - Review sign-in logs for suspicious activity (new devices, impossible travel, MFA prompts, unusual IPs)
- Mailbox and persistence checks:
  - Review for suspicious inbox rules, forwarding, OAuth grants, or abnormal mailbox access
- Enterprise hunt:
  - Search for indicators across email logs, proxy/DNS logs, and endpoint telemetry where applicable

## IOC Summary (Sanitized)
Indicators captured in the project README and triage note. If needed, record IOCs in a case-specific tracker (sanitized) for containment and hunting.
