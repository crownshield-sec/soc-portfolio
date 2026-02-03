# Wireshark Investigation Notes (Lab)

## Goal
Validate whether the observed traffic supports the alert hypothesis (trojanized download / malicious outbound behavior) and extract actionable indicators for escalation.

## Approach
- Anchored the timeline around download and first execution.
- Identified destinations and protocols used post-execution.
- Extracted candidate indicators and assessed whether activity was expected or anomalous.

## Key Checks
- DNS: newly queried domains, unusual TLDs, randomized subdomains, repeated lookups
- HTTP/HTTPS: unusual paths, repeated requests, uncommon destinations
- TLS: SNI values (if present), destination reputation via OSINT
- Frequency: periodic connections suggesting beacon-like behavior

## Filters Used (Examples)
- `dns`
- `http`
- `tls`
- `ip.addr == <SANITIZED_IP>`
- `dns.qry.name contains "<SANITIZED_DOMAIN>"`

## Observations (Sanitized)
- Outbound connections observed to <SANITIZED_DOMAIN> / <SANITIZED_IP>.
- Network activity begins shortly after execution timeframe.
- Connection pattern suggests staging/beaconing (if applicable).

## Indicators Extracted
- Domains: <SANITIZED_DOMAIN_1>, <SANITIZED_DOMAIN_2>
- IPs: <SANITIZED_IP_1>
- URLs: <SANITIZED_URL_1> (if observed)
- File hash: <SANITIZED_HASH> (if available)

## OSINT Enrichment (Summary)
- VirusTotal: <brief sanitized verdict summary>
- Talos: <brief sanitized reputation summary>

## Triage Conclusion
- Confidence: Low / Medium / High
- Severity: Low / Medium / High / Critical
- Rationale: <1–3 sentences>
