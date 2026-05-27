# Phishing Triage Mini-Report 

## Investigation Workflow
Investigation artifacts and analyst documentation:
1. [`triage-note.md`](triage-note.md)
2. [`email-artifact-review.md`](email-artifact-review.md)
3. [`ioc-tracking.csv`](ioc-tracking.csv)
4. [`escalation-summary.md`](escalation-summary.md)


## Objective
**Demonstrates analyst triage workflow including indicator extraction, risk assessment, containment recommendations, and escalation-ready documentation.

## Scenario (Sanitized)
A user reported a suspicious email claiming urgency and requesting action via a link. The objective was to triage the message, assess risk, extract indicators, and recommend containment and user guidance.

## Analyst Investigation Workflow
- Reviewed email header and body artifacts (sanitized) to assess legitimacy and delivery path.
- Analyzed the lure technique and likely attacker objective (credential capture, malware delivery, or payment fraud).
- Extracted and documented indicators (sender artifacts, domains, URLs, and any related infrastructure) using safe sanitization.
- Produced containment recommendations and escalation notes suitable for Level 2 follow-up.

## Investigation Findings
- Primary indicators: `<SANITIZED_DOMAIN_1>`, `<SANITIZED_SENDER>`, `<SANITIZED_URL_1>` (if observed)
- Probable objective: `<SANITIZED_OBJECTIVE>` (e.g., credential harvesting or malware delivery)
- Risk rationale: message content + urgency/lure pattern + indicator reputation and/or mismatched sender/authentication cues

## Containment & Escalation Recommendations
- Containment: block identified domains/URLs at email security/DNS/proxy as appropriate; quarantine similar messages.
- User guidance: do not click; report similar emails; reset credentials if interaction occurred; enable MFA if not already enabled.
- Detection improvements: add rules for similar sender patterns, subject/lure keywords, and newly observed domains; tune for false positives.

## ## Skills Demonstrated
- Phishing triage
- IOC extraction and tracking
- Security investigation workflows
- Incident documentation
- Risk assessment
- Escalation analysis
- Containment recommendations
- Analyst reporting
