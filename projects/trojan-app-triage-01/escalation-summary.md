# Escalation Summary — Trojanized Productivity App (Lab)

## Executive Summary
A user-installed “productivity” application triggered a security alert for suspicious outbound traffic. Network analysis and OSINT enrichment indicate a likely trojanized installer or post-execution beaconing. Recommend containment and Level 2 follow-up for host triage and environment-wide hunting.

## Timeline (Sanitized)
- T0: User download initiated
- T1: Application executed
- T2: Alert generated for suspicious outbound connections
- T3: Wireshark review and IOC extraction completed
- T4: OSINT enrichment completed; escalation prepared

## Key Findings
- Outbound communication to suspicious/low-reputation infrastructure (<SANITIZED_DOMAINS/IPs>).
- Connection pattern consistent with follow-on staging or beaconing (if observed).
- OSINT (VirusTotal/Talos) supports elevated risk assessment.

## Scope (Initial)
- Affected endpoint: 1 workstation (user-reported)
- Lateral movement: Unknown at Level 1
- Data exposure: Unknown at Level 1

## Recommended Containment (Immediate)
- Isolate/quarantine affected endpoint (EDR isolation if available).
- Block confirmed malicious domains/IPs at DNS/proxy/firewall.
- Reset user credentials if credential exposure is suspected.

## Level 2 Requested Actions
- Host triage: persistence checks, autoruns/services, scheduled tasks, suspicious binaries, EDR telemetry review.
- Enterprise hunt: search for IOCs and similar connection patterns across endpoints.
- Confirm whether a second-stage payload executed and whether persistence was established.

## IOC Summary (Sanitized)
See `ioc-tracking.csv` for recorded indicators and enrichment notes.
