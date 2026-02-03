# Incident Triage Note (Lab)

## Summary
- Date/Time: <SANITIZED_DATE_TIME>
- Report source (SIEM/EDR/user report): SIEM alert (suspicious outbound domain / possible C2)
- Category: Suspected Malware / Trojan
- Severity: High (user-executed + suspicious outbound activity)
- Affected asset(s): 1 workstation (<SANITIZED_HOSTNAME>), 1 user (<SANITIZED_USER>)
- Status: Escalated to Level 2 (containment recommended)

## Initial Observation
- What triggered the alert:
  - SIEM flagged outbound connections to suspicious/low-reputation infrastructure shortly after the user installed and executed a “productivity” application.
- Why it matters (risk):
  - Post-execution callbacks can indicate a trojanized installer, staged payload retrieval, or command-and-control activity.

## Evidence Collected (Sanitized)
- Logs / telemetry reviewed:
  - SIEM event context (destination domain/IP, timestamps, frequency/connection count)
  - DNS query activity for <SANITIZED_DOMAIN_1> and <SANITIZED_DOMAIN_2>
- Network capture reviewed:
  - Wireshark review of post-execution traffic window (pcap)
  - Note: Traffic is largely TLS-encrypted; analysis relies on DNS pivots, destination IP correlation, timing, and connection patterns rather than URL paths.
- Indicators (domains/IPs/hashes):
  - Domains: <SANITIZED_DOMAIN_1>, <SANITIZED_DOMAIN_2>
  - IP: <SANITIZED_IP_1>
  - File hash: <SANITIZED_HASH> (only if obtained from installer/endpoint telemetry)

## Analysis
- Likely impact:
  - Suspected compromise is limited to one endpoint at time of triage; credential exposure and secondary payload risk cannot be ruled out without host validation.
- Confidence and rationale:
  - Confidence: Medium–High
  - Rationale: Strong temporal correlation (execution → alert → outbound traffic), suspicious destination reputation, and observed connection behavior consistent with callback/beacon-like activity.

## Recommended Next Actions
- Immediate containment:
  - Isolate endpoint via EDR (or remove from network) pending validation.
  - Block identified domains at DNS/proxy and destination IP at firewall, as appropriate.
  - Preserve evidence: retain pcap, SIEM alert context, and installer artifact (if available).
- Further investigation pivots:
  - Confirm initiating process (EDR process tree/command line) and align with network timestamps.
  - Check persistence mechanisms (autoruns/services/scheduled tasks).
  - Hunt enterprise-wide for the same domains/IP and similar outbound patterns.
- Remediation suggestions:
  - Remove malicious artifacts; reimage if required by policy and findings.
  - Credential reset if host review indicates credential access risk.
- Detection improvement ideas:
  - Add detection for suspicious post-install outbound patterns from new/unsigned executables.
  - Alert on newly observed domains contacted immediately after software execution (tuned to reduce false positives).

## Escalation Decision
- Escalate to Level 2: Yes
- Reason for escalation:
  - Suspected malware with outbound behavior consistent with callback activity; requires host-based confirmation and environment scoping beyond Level 1.
- What Level 2 should do next:
  - Acquire host triage artifacts (process tree, hashes, persistence checks, EDR timeline).
  - Determine whether secondary payload(s) executed and whether persistence was established.
  - Validate scope across the environment and confirm block/isolation actions are complete.
