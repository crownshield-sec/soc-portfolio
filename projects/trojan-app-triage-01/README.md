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

- Reviewed the alert context and formed an initial triage hypothesis.
- Analyzed network traffic in Wireshark to identify:
  - DNS queries and suspicious domain patterns
  - HTTP(S) requests and destination infrastructure
  - Connection frequency and timing patterns to assess possible beaconing
- Extracted available indicators, including domains and IP addresses, and recorded them in an IOC tracker.
- Enriched indicators using VirusTotal and Cisco Talos and assessed their reputation and known associations.
- Determined the incident severity and recommended containment actions.
- Produced a concise Level 2 escalation package containing findings, scope assumptions, and recommended investigative pivots.

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

### Reasoning for escalation

- The network activity occurred shortly after execution of the downloaded application.
- DNS and HTTPS communication patterns were inconsistent with expected business use.
- Repeated outbound connections indicated possible beaconing or command-and-control activity.
- OSINT enrichment identified suspicious or low-reputation infrastructure associated with the observed indicators.
- Level 1 did not have sufficient endpoint telemetry to confirm process execution, persistence, payload activity, or the full scope of compromise.
- The available evidence justified immediate containment and deeper host-based investigation.

### Level 1 stop condition — when I would not escalate

I would close or downgrade the alert if:

- The application source and file were conclusively validated as legitimate.
- The observed destinations were verified as approved vendor infrastructure.
- The network traffic matched documented application behavior.
- No suspicious child processes, persistence mechanisms, credential access, or abnormal outbound activity were identified.
- OSINT and internal threat-intelligence checks produced no adverse findings.

### Possible Level 2 validation

- **Endpoint validation:** Review EDR telemetry, process trees, command-line activity, file creation, registry modifications, and persistence mechanisms.
- **File analysis:** Retrieve the downloaded file and validate its hash, signature, metadata, and sandbox behavior.
- **Scope assessment:** Search for the same file hash, domain, IP addresses, URLs, process names, and behaviors across the environment.
- **Persistence review:** Examine scheduled tasks, services, startup folders, registry run keys, and newly installed applications.
- **Credential exposure:** Review suspicious authentication activity and reset credentials if credential theft is suspected.
- **Network containment:** Block confirmed malicious indicators at DNS, proxy, firewall, and endpoint controls.

## Sanitization Notes
All identifiers (usernames, hostnames, IPs, domains, timestamps, hashes) are anonymized or replaced with representative values to prevent disclosure of sensitive information.
