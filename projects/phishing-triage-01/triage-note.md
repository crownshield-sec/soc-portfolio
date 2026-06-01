# SOC Escalation Summary — Phishing Investigation

## Executive Summary


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
Level 1 triage completed. Indicators extracted and documented. Containment recommendations developed. Escalation to Level 2 is conditionally recommended pending user exposure validation and scope assessment.

## Initial Observation
- What triggered the alert/report:
  - User reported a suspicious message with urgency and a call-to-action link.
- Why it matters (risk):
  - Phishing may enable credential theft, malware delivery, or business process compromise.

Indicators Extracted

Sender / From:
support@secure-alerts-example[.]com

Reply-To:
alerts-example-mail[.]com

Domains:
- secure-alerts-example[.]com
- alerts-example-mail[.]com

URL(s):
- account-verification-login[.]com

Attachment:
- None observed

## Analyst Assessment
- Probable Objective: Credential Harvesting
- Confidence and rationale:
  - Confidence: Medium–High
  - Rationale:
    The message contained multiple phishing indicators including urgency-based social engineering language, suspicious sender infrastructure, domain mismatches, and an external credential collection URL. These characteristics are commonly associated with credential harvesting campaigns.

## Recommended Response Actions
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
Escalate to Level 2: Conditional

Reason:
Escalation is recommended if user interaction occurred, credentials may have been exposed, additional recipients are identified, or related phishing activity is observed elsewhere in the environment.

- Level 2 requested follow-up (if escalated):
  - Review identity sign-in logs for suspicious access.
  - Conduct mailbox rule review and identify any follow-on phishing or persistence attempts.
  - Confirm enterprise-wide containment and monitor for repeat campaigns.
