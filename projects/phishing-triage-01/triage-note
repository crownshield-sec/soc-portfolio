# Incident Triage Note — Phishing Email (Lab)

## Summary
- Date/Time: <SANITIZED_DATE_TIME>
- Report source: User report and/or email security alert
- Category: Phishing (suspected)
- Severity: Medium–High (depends on user interaction and indicator risk)
- Affected asset(s): 1 user (<SANITIZED_USER>), mailbox (<SANITIZED_MAILBOX>)
- Status: Triage complete; containment recommended; escalate to Level 2 if exposure is suspected

## Initial Observation
- What triggered the alert/report:
  - User reported a suspicious message with urgency and a call-to-action link.
- Why it matters (risk):
  - Phishing may enable credential theft, malware delivery, or business process compromise.

## Evidence Collected (Sanitized)
- Email artifacts reviewed:
  - Subject/sender display name vs. sender address alignment
  - Reply-To and link destination mismatch checks
  - Header authentication signals (SPF/DKIM/DMARC results if available)
- Indicators extracted:
  - Sender / From: `<SANITIZED_SENDER>`
  - Reply-To: `<SANITIZED_REPLYTO>` (if present)
  - Domains: `<SANITIZED_DOMAIN_1>`, `<SANITIZED_DOMAIN_2>`
  - URL(s): `<SANITIZED_URL_1>` (if explicitly observed)
  - Attachment: `<SANITIZED_ATTACHMENT_NAME>` (if present)

## Analysis
- Probable objective:
  - `<SANITIZED_OBJECTIVE>` (credential harvesting, malware delivery, payment fraud, etc.)
- Confidence and rationale:
  - Confidence: Medium–High
  - Rationale: lure characteristics + indicator reputation and/or authentication anomalies + destination mismatch patterns

## Recommended Next Actions
- Immediate containment:
  - Quarantine the email and search for similar messages across mailboxes (same sender/domain/subject).
  - Block domains/URLs at email security gateway, DNS/proxy, and web filtering as applicable.
- User guidance:
  - If no interaction: advise user to delete/report and remain vigilant for follow-up attempts.
  - If link clicked or credentials entered: initiate credential reset, review sign-in logs, and enforce MFA.
- Investigation pivots:
  - Confirm whether any users clicked the link or entered credentials.
  - Review email gateway telemetry for delivery scope and any additional recipients.

## Escalation Decision
- Escalate to Level 2: <YES/NO>
- Reason:
  - Escalate if user interaction occurred, credentials may be exposed, or indicators show high risk.
- Level 2 requested follow-up (if escalated):
  - Review identity sign-in logs for suspicious access.
  - Conduct mailbox rule review and identify any follow-on phishing or persistence attempts.
  - Confirm enterprise-wide containment and monitor for repeat campaigns.
