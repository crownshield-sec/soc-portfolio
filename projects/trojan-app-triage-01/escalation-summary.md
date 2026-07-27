# Escalation Summary — Trojanized Productivity App (Lab)

## Executive Summary

A user-installed “productivity” application generated a SIEM alert for suspicious outbound network activity shortly after execution. Wireshark analysis and OSINT enrichment identified activity consistent with a potentially trojanized installer or post-execution callback behavior. Immediate containment of the affected endpoint and Level 2 validation are recommended to determine host impact and broader environmental scope.

## Timeline (Sanitized)

- **T0:** User initiated the application download.
- **T1:** Application was executed.
- **T2:** SIEM generated an alert for suspicious outbound connections.
- **T3:** Network traffic was reviewed in Wireshark and indicators were extracted.
- **T4:** Indicators were enriched using VirusTotal and Cisco Talos, and the escalation package was prepared.

## Key Findings

- Post-execution outbound communications correlated with the SIEM alert window.
- DNS pivots and destination-IP correlation identified suspicious external infrastructure.
- Traffic was largely TLS-encrypted; analysis relied on timestamps, DNS activity, destination correlation, and connection patterns rather than decrypted content or URL paths.
- OSINT enrichment supported an elevated risk classification.
- Packet evidence alone did not conclusively confirm command-and-control activity.

## Scope (Initial)

- **Affected endpoint(s):** 1 workstation associated with the SIEM alert
- **Affected user(s):** 1 sanitized user
- **Lateral movement:** Unknown at Level 1
- **Data exposure:** Unknown at Level 1
- **Additional affected systems:** Not confirmed at Level 1

## Recommended Containment (Immediate)

- Isolate or quarantine the endpoint using EDR, if available, pending validation.
- Block the identified domains at DNS and proxy controls and the destination IP at the firewall, as appropriate.
- Preserve the PCAP and SIEM alert context.
- Acquire and retain the installer artifact if it becomes available during Level 2 investigation.
- Reset affected credentials if host review identifies credential-access risk.

## Level 2 Requested Actions

### Host-Based Confirmation

- Identify the process tree responsible for the outbound connections, including parent process, child processes, and command-line activity.
- Validate persistence mechanisms, including services, scheduled tasks, startup locations, and autoruns.
- Determine whether secondary payloads were downloaded, dropped, or executed.
- Acquire the installer file and validate its hash, metadata, digital signature, and sandbox behavior.

### Scope and Hunt

- Search enterprise telemetry for matching domains, IP addresses, and similar outbound connection patterns.
- Identify additional endpoints exhibiting the same DNS queries or destination contacts.
- Review related authentication activity for possible credential exposure.

### Remediation Decision

- Determine whether removal and cleanup are sufficient or whether reimaging is required under organizational policy.
- Confirm that containment and blocking actions have been completed.

## Indicators (Sanitized)

See `ioc-tracking.csv` for recorded indicators, confidence, severity, enrichment sources, and recommended actions.
