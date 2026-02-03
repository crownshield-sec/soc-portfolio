# Incident Triage Note (Lab)

## Summary
- Date/Time: <SANITIZED_DATE_TIME>
- Report source (SIEM/EDR/user report): SIEM alert (suspicious outbound domain / possible C2)
- Category: Suspected Malware / Trojan
- Severity: High (user-executed + suspicious outbound behavior)
- Affected asset(s): 1 workstation (<SANITIZED_HOSTNAME>), 1 user (<SANITIZED_USER>)
- Status: Escalated to Level 2 (containment recommended)

## Initial Observation
- What triggered the alert:
  - SIEM flagged outbound connections to a suspicious/low-reputation domain shortly after the user installed and executed a “productivity” application.
- Why it matters (risk):
  - User execution + immediate outbound communications may indicate trojanized installer, beaconing, or staged payload activity.

## Evidence Collected (Sanitized)
- Logs / telemetry reviewed:
  - SIEM event details (destination domain/IP, timestamps, connection count)
  - DNS query activity for <SANITIZED_DOMAIN>
- Network capture reviewed:
  - Wireshark review of post-execution traffic window (pcap)
- Indicators (IPs/domains/hashes):
  - Domain(s): <SANITIZED_DOMAIN_1>, <SANITIZED_DOMAIN_2>
  - IP(s): <SANITIZED_IP_1>
  - URL(s): 
  - Hash: <SANITIZED_HASH> (if applicable)

## Analysis
- Likely impact:
  - Suspected compromise limited to one endpoint at time of triage; potential credential exposure and follow-on payload risk cannot be ruled out.
- Confidence and rationale:
  - Confidence: Medium–High
  - Rationale: Temporal correlation between execution and outbound traffic + suspicious destination reputation + traffic pattern consistent with callback/beaconing.

## Recommended Next Actions
- Immediate containment:
  - Isolate endpoint via EDR (or remove from network) pending validation.
  - Block confirmed malicious domains/IPs at DNS/proxy/firewall as appropriate.
  - Preserve evidence: retain pcap, logs, and installer artifact (if available).
- Further investigation pivots:
  - Confirm process initiating the connection (EDR/network telemetry correlation).
  - Check for persistence mechanisms (autoruns/services/scheduled tasks).
  - Hunt enterprise-wide for same domains/IPs and similar traffic pattern.
- Remediation suggestions:
  - Remove malicious artifacts; reimage if required by policy.
  - Credential reset if signs of credential access exist.
- Detection improvement ideas:
  - Add detection for similar newly registered domains / suspicious outbound patterns.
  - Alert on unusual post-install network activity for unsigned/new executables.

## Escalation Decision
- Escalate to Level 2: Yes
- Reason for escalation:
  - Suspected malware with outbound communications consistent with command-and-control behavior; requires host-based confirmation and broader hunting.
- What Level 2 should do next:
  - Acquire host triage artifacts (process tree, file hashes, persistence checks, EDR timeline).
  - Determine whether stage-2 payload executed and whether lateral movement occurred.
  - Validate scope across environment and confirm block actions are complete.
