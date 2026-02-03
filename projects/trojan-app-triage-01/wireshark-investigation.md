# Wireshark Investigation Notes (Lab)

## Case Context (Sanitized)
A user downloaded and executed a “productivity” application. Shortly after execution, monitoring generated an alert for suspicious outbound network activity consistent with malware callback behavior. The goal of this review was to validate the alert hypothesis using network evidence, extract indicators, and produce investigation notes suitable for escalation.

## Objective
1) Confirm whether post-execution network activity is consistent with trojanized behavior.  
2) Identify and document actionable indicators (domains/IPs/URLs) for containment and hunting.  
3) Provide clear pivots and next investigative steps for Level 2.

## Data Reviewed (Sanitized)
- Source: Packet capture (pcap) covering the period surrounding download/execution and alert time.
- Scope: Single endpoint traffic window (workstation) with focus on outbound communications.
- Artifacts produced: Indicator list recorded in `ioc-tracking.csv`.

## Investigation Method
### Step 1 — Establish the time window
- Anchored analysis around:
  - Reported execution time (T1)
  - Alert generation time (T2)
- Focused on the first outbound activity immediately after execution to identify potential initial callbacks.

### Step 2 — Identify “first suspicious destinations”
- Reviewed DNS activity to identify:
  - Newly queried domains that correlate to post-execution traffic
  - Unusual domains or uncommon patterns (e.g., new infrastructure, suspicious naming)
- Traced follow-on communications to destination IPs and protocols used.

### Step 3 — Validate behavior patterns
- Looked for signals consistent with malware stages:
  - Beaconing (regular interval connections)
  - Staging (download of additional content)
  - Command-and-control indicators (repeated callback to a domain/IP, unusual request patterns)

### Step 4 — Extract indicators and document pivots
- Recorded primary indicators:
  - `<SANITIZED_DOMAIN>` (primary C2 candidate)
  - `<SANITIZED_DOMAIN_2>` (secondary domain)
  - `<SANITIZED_IP_1>` (destination IP)
  - `<SANITIZED_URL_1>` (if explicitly observed)
- Documented recommended containment actions (DNS/proxy/firewall blocks) and hunting pivots.

## Filters and Views Used (Examples)
> Note: filters are representative of repeatable SOC workflow patterns.

- Baseline protocol filters:
  - `dns`
  - `http`
  - `tls`
- IOC-focused filters:
  - `dns.qry.name contains "<SANITIZED_DOMAIN>"`
  - `ip.addr == <SANITIZED_IP_1>`
- Timeline scoping:
  - Narrow to the time window around alert/execution and review first occurrences of suspicious traffic.

## Key Findings (Sanitized)
### 1) DNS activity supports post-execution pivot
- DNS queries for `<SANITIZED_DOMAIN>` and `<SANITIZED_DOMAIN_2>` occur in the post-execution window.
- The timing aligns closely with the alert window, supporting the hypothesis of application-triggered outbound communication.

**Assessment:** DNS activity provides a reliable pivot for identifying related connections and scoping additional telemetry.

### 2) Outbound traffic to suspicious destination infrastructure
- The endpoint initiates outbound communications to `<SANITIZED_IP_1>` associated with the suspicious domains.
- The behavior appears abnormal relative to typical “productivity” application traffic patterns.

**Assessment:** Destination infrastructure is likely relevant to the alert; treat as potentially malicious until confirmed otherwise.

### 3) Connection behavior indicates possible callback/beaconing
- Observed repeated outbound communication patterns in the post-execution window (if present).
- Where applicable, traffic resembles:
  - short repetitive sessions, or
  - periodic connections, or
  - consistent destination contact shortly after execution

**Assessment:** Pattern is consistent with callback or beacon-like behavior, raising the likelihood of trojanized or staged malware activity.

### 4) URL-level detail (only if explicitly observed)
- If the capture contains explicit HTTP requests or visible URIs, record the suspicious request path as `<SANITIZED_URL_1>`.
- If most traffic is encrypted (TLS), rely on DNS + destination IP + timing correlation rather than inventing URL paths.

**Assessment:** URL-level evidence increases confidence, but absence of a URL is common when traffic is encrypted.

## Indicator Extraction (Recorded in `ioc-tracking.csv`)
- Domain (primary): `<SANITIZED_DOMAIN>`  
- Domain (secondary): `<SANITIZED_DOMAIN_2>`  
- Destination IP: `<SANITIZED_IP_1>`  
- URL (optional): `<SANITIZED_URL_1>`  
- File hash (optional): `<SANITIZED_SHA256>` (if obtained from installer/dropped file)

## OSINT Enrichment Guidance (Summary)
- VirusTotal:
  - Check domain/IP detections, associated files, and communicating samples.
  - Use relationship graphs (if available) to identify additional infrastructure.
- Talos:
  - Validate reputation and categorize domain/IP risk.
  - Note any indicators tied to known threat activity.

**Outcome expectation:** If OSINT indicates malicious or suspicious reputation, raise confidence and strengthen containment recommendations.

## Triage Conclusion
- Severity: **High**
  - User executed untrusted software + post-execution outbound activity to suspicious infrastructure.
- Confidence: **Medium–High**
  - Strong temporal correlation between execution and outbound indicators; suspicious destinations support escalation.

## Recommended Actions (SOC Level 1 → Level 2 Handoff)
### Immediate containment (Level 1 recommendation)
- Isolate endpoint (EDR isolation or remove from network) pending confirmation.
- Block indicators:
  - DNS/proxy block for `<SANITIZED_DOMAIN>` and `<SANITIZED_DOMAIN_2>`
  - Firewall block for `<SANITIZED_IP_1>`
- Preserve evidence:
  - Save pcap, SIEM alert context, and any installer artifact (if available).

### Level 2 requested follow-up
- Host-based confirmation:
  - Identify parent process initiating outbound traffic (process tree + command line).
  - Check persistence (autoruns/services/scheduled tasks).
  - Validate whether additional payloads were dropped or executed.
- Scope/hunt:
  - Search enterprise telemetry for the same domains/IPs and similar patterns.
  - Identify other endpoints with matching DNS queries or outbound destinations.

## Notes on Sanitization
All indicators, hostnames, user identifiers, and timestamps are sanitized. This project demonstrates repeatable SOC workflow: alert context → network validation → IOC extraction → escalation-ready documentation.
