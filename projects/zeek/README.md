# Zeek Investigation — Network Connection Analysis

## Investigation Objective

Analyze Zeek network logs to identify connection activity, protocol behavior, source and destination communication patterns, and potential indicators of suspicious network behavior.

## Investigation Scenario

Network telemetry was reviewed using Zeek to understand host communication patterns, identify observed services, and document connection-level metadata suitable for SOC analysis and escalation review.

## Analyst Investigation Workflow

- Reviewed Zeek network connection logs.
- Identified source and destination IP communication.
- Analyzed protocol and service metadata.
- Reviewed connection duration, byte counts, and connection states.
- Documented findings and analyst interpretation.

## Zeek Logs Reviewed

- conn.log
- dns.log
- http.log
- ssl.log

## Tools & Technologies

- Zeek
- Linux command line
- jq / text parsing
- Network telemetry analysis

## Skills Demonstrated

- Network metadata analysis
- Connection log review
- Protocol investigation
- Source and destination IP analysis
- Security monitoring workflows
- Analyst documentation
