# Trojanized Productivity App Download — Alert Triage & Escalation (Lab)

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

## Artifacts in This Folder
- `triage-note.md` — Incident triage note (sanitized)
- `wireshark-investigation.md` — Wireshark analysis notes and pivot logic
- `ioc-tracking.csv` — Sanitized IOC tracking table
- `escalation-summary.md` — Level 2 escalation summary (sanitized)

## Sanitization Notes
All identifiers (usernames, hostnames, IPs, domains, timestamps, hashes) are anonymized or replaced with representative values to prevent disclosure of sensitive information.
