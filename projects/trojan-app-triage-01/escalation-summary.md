# Escalation Summary — Trojanized Productivity App (Lab)

## Executive Summary
A user-installed “productivity” application generated an alert for suspicious outbound network activity shortly after execution. Wireshark review and OSINT enrichment indicate behavior consistent with a trojanized installer and/or post-execution callback activity. Recommend immediate containment of the endpoint and Level 2 validation for host impact and broader scope.

## Timeline (Sanitized)
- T0: User download initiated
- T1: Application executed
- T2: Alert generated for suspicious outbound connections
- T3: Network traffic reviewed in Wireshark; indicators extracted
- T4: Indicators enriched via OSINT (VirusTotal/Talos); escalation prepared

## Key Findings
- Post-execution outbound communications correlated with the alert window.
- DNS pivots and destination IP correlation identify suspicious external infrastructure (sanitized).
- Traffic was largely TLS-encrypted; validation relied on timing, DNS, destination IPs, and connection patterns rather than URL paths.
- OSINT enrichment supports elevated risk classification.

## Scope (Initial)
- Affected endpoint(s): 1 workstation (user-reported)
- Affected user(s): 1 user (sanitized)
- Lateral movement: Unknown at Level 1
- Data exposure: Unknown at Level 1

## Recommended Containment (Immediate)
- Isolate/quarantine the endpoint (EDR isolation if available) pending validation.
- Block identified domain(s) at DNS/proxy and destination IP(s) at firewall, as appropriate.
- Preserve evidence (pcap, alert context, and installer artifact if available).
- Initiate credential reset if host review indicates credential access risk.

## Level 2 Requested Actions
- Host-based confirmation:
  - Identify process tree responsible for outbound connections (parent/child, command line).
  - Validate persistence mechanisms (services, scheduled tasks, autoruns).
  - Determine whether secondary payload(s) were dropped or executed.
- Scope and hunt:
  - Search enterprise telemetry for matching domains/IPs and similar outbound patterns.
  - Identify additional endpoints exhibiting the same DNS queries or destination contacts.
- Remediation decision:
  - Confirm eradication approach (clean/remove vs. reimage) based on findings and policy.

## Indicators (Sanitized)
See `ioc-tracking.csv` for recorded indicators and enrichment notes.
