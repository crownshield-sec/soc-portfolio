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

## Connection Analysis

The Zeek connection log was reviewed to identify source and destination communications, protocols, and observed services during packet capture analysis.


### Connection Log Review

<a href="images/zeek-conn-analysis.png">
  <img src="images/zeek-conn-analysis.png" width="1000">
</a>

## HTTP Analysis

The Zeek HTTP log was reviewed to identify web requests, response codes, and application-layer metadata observed during packet capture analysis.

### HTTP Log Review

<a href="images/zeek-http-analysis.png">
  <img src="images/zeek-http-analysis.png" width="1000">
</a>

### Findings

The HTTP log identified successful web communications originating from the monitored host.

| Observation | Details |
|------------|------------|
| Source Host | 172.30.126.212 |
| Protocol | HTTP |
| Response Status | 200 OK |
| HTTP Version | 1.1 |
| Content Type | application/x-debian-package |

The observed traffic was consistent with Ubuntu package repository communications generated during system package installation activities. No suspicious HTTP requests or anomalous response codes were identified.

### Findings

The connection log identified the following communication patterns:

| Source IP | Destination IP | Protocol | Service | Observation |
|------------|------------|------------|------------|------------|
| 172.30.126.212 | 185.125.190.57 | UDP | NTP | Normal time synchronization activity |
| 172.30.126.212 | 104.20.23.154 | TCP | HTTP | Web communication observed |
| 172.30.126.212 | 172.66.152.176 | TCP | HTTP | HTTP traffic associated with testing activity |
| 172.30.126.212 | 142.251.34.142 | ICMP | Ping | Connectivity testing with Google |

No suspicious network connections were identified during this review.

## Skills Demonstrated

- Network metadata analysis
- Connection log review
- Protocol investigation
- Source and destination IP analysis
- Security monitoring workflows
- Analyst documentation
