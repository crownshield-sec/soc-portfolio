# Trojanized Productivity App Download — Alert Triage & Escalation (Lab)
## Start here (recommended reading order)

1. **Triage Note** → [triage-note.md](./triage-note.md)  
2. **Wireshark Investigation Notes** → [wireshark-investigation.md](./wireshark-investigation.md)  
3. **IOC Tracker** → [ioc-tracking.csv](./ioc-tracking.csv)  
4. **Escalation Summary** → [escalation-summary.md](./escalation-summary.md)

---
## What each file contains (quick map)

- **triage-note.md**: initial alert context, risk framing, evidence collected, and the Level 1 decision to escalate.  
- **wireshark-investigation.md**: how you validated the alert using DNS/IP/timing pivots (and TLS constraints), plus investigation pivots for Level 2.  
- **ioc-tracking.csv**: sanitized indicators + source + severity + recommended blocks/actions.  
- **escalation-summary.md**: executive-ready handoff (timeline, key findings, containment, and Level 2 requested actions).

## Objective
Demonstrate SOC Level 1 alert triage and escalation decision-making by validating a suspected trojanized application download using network evidence (Wireshark) and OSINT enrichment (VirusTotal/Talos), then producing an escalation-ready incident package.

## Scenario (Sanitized)
A user downloaded a “productivity” application to improve work efficiency. Shortly after execution, security monitoring generated an alert for suspicious outbound network activity consistent with malware behavior. The goal was to triage the alert, extract and enrich indicators, recommend containment, and prepare a Level 2 escalation summary.

## Evidence (Sanitized)
- Network capture reviewed in Wireshark (pcap)
- Observed DNS/HTTP(S) indicators and connection patterns
- OSINT enrichment of domains/IPs/hashes using VirusTotal and/or Cisco Talos

## What I Did (SOC Level 1 Workflow)
- Reviewed alert context and formed initial triage hypothesis.
- Analyzed network traffic in Wireshark to identify:
  - DNS queries and suspicious domain patterns
  - HTTP(S) requests and destination infrastructure
  - Repetitive beacons / abnormal connection frequency (if present)
- Extracted indicators (domains, IPs, URLs, file hash if available) and recorded them in an IOC tracker.
- Enriched indicators using VirusTotal/Talos and assessed reputation/associations.
- Determined severity and recommended containment steps.
- Produced a concise escalation package for Level 2 with findings, scope assumptions, and next investigative pivots.

## Findings (Summary)
- Indicators and network behavior were consistent with a trojanized installer or post-execution beaconing.
- OSINT enrichment supported elevated risk (e.g., malicious/low reputation infrastructure, known associations, or suspicious hosting patterns).
- The incident warranted escalation for deeper host-based validation and enterprise-wide hunting.

## Recommended Actions
- Contain affected endpoint (isolation/quarantine), reset credentials if exposure is suspected.
- Block confirmed malicious domains/IPs at DNS/proxy/firewall (as appropriate).
- Level 2 follow-up: collect host triage artifacts, validate persistence, and run environment-wide searches for matching IOCs and behaviors.

## Decision (SOC Level 1)
**Disposition:** Escalated to Level 2

**Reasoning (why escalate):**
- The email exhibits phishing indicators (lure + suspicious link/sender artifacts) with potential for credential capture or follow-on compromise.
- Exposure is not fully confirmed at Level 1 (unknown click/credential entry), and validation requires deeper telemetry review.
- Indicators warrant containment actions (quarantine + block) and environment scoping to prevent campaign spread.

**Level 1 stop condition (when I would NOT escalate):**
- The message is conclusively benign (validated sender + alignment with business context) **and**
- No interaction occurred **and**
- No similar messages are present in the environment after a quick gateway/mailbox search.

**Possible Level 2 validation:**
- **Exposure confirmation:** user interaction status (clicked link, entered credentials, opened attachment).
- **Message scope:** search mail gateway and mailboxes for matching sender/subject/URL patterns (campaign suppression).
- **Identity risk:** review sign-in logs for abnormal activity (new device, impossible travel, MFA prompts, suspicious IPs).
- **Mailbox tampering:** check for inbox rules, forwarding, OAuth app grants, unusual mailbox access.
- **IOC expansion:** enrich domains/URLs/IPs and identify related infrastructure for broader hunting.

## Artifacts in This Folder
- `triage-note.md` — Incident triage note (sanitized)
- `wireshark-investigation.md` — Wireshark analysis notes and pivot logic
- `ioc-tracking.csv` — Sanitized IOC tracking table
- `escalation-summary.md` — Level 2 escalation summary (sanitized)

## Sanitization Notes
All identifiers (usernames, hostnames, IPs, domains, timestamps, hashes) are anonymized or replaced with representative values to prevent disclosure of sensitive information.
