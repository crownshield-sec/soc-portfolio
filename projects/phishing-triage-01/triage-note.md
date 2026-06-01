# SOC Escalation Summary — Phishing Investigation

## Summary
Summary

Date/Time:
Sanitized for public release

Report Source:
User report

Category:
Phishing Email

Severity:
High

Affected Assets:
One reported user mailbox

Status:
Triage completed. Indicators extracted. Containment recommendations documented. Escalation to Level 2 recommended pending user exposure validation.

## Initial Observation
- What triggered the alert/report:
  - User reported a suspicious message with urgency and a call-to-action link.
- Why it matters (risk):
  - Phishing may enable credential theft, malware delivery, or business process compromise.

### Indicators Extracted

- Sender / From: support@secure-alerts-example[.]com
- Reply-To: alerts-example-mail[.]com
- Domains:
  - secure-alerts-example[.]com
  - alerts-example-mail[.]com
- URL(s):
  - account-verification-login[.]com
- Attachment:
  - None observed

## Analysis
- Probable objective: Credeential Harvesting
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
- Escalate to Level 2: YES
- Reason:
  - Escalate if user interaction occurred, credentials may be exposed, or indicators show high risk.
- Level 2 requested follow-up (if escalated):
  - Review identity sign-in logs for suspicious access.
  - Conduct mailbox rule review and identify any follow-on phishing or persistence attempts.
  - Confirm enterprise-wide containment and monitor for repeat campaigns.
