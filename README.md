# SOC Portfolio (Splunk • Wireshark • TheHive)

Lab-based SOC portfolio demonstrating repeatable security operations workflows: alert triage, investigation, documentation, and escalation. Artifacts are written in an analyst style and structured to resemble SOC Level 1 handoffs.

## Focus Areas
- Alert triage, severity assessment, and escalation decision-making  
- Log analysis and correlation (Splunk-style searching)  
- Packet analysis and timeline development (Wireshark)  
- Case documentation workflows (TheHive-style case notes)

## Projects
1) **Phishing Triage Mini-Report**
   - Path: `projects/phishing-triage-01/README.md`
   - Focus: email artifact review, indicator extraction, and containment recommendations

2) **SIEM Query Practice (Splunk) — Suspicious Authentication**
   - Path: `projects/splunk-detections-01/README.md`
   - Focus: SPL-style searches, correlation logic, and triage-ready summaries

3) **Case Documentation (TheHive)**
   - Path: `projects/thehive-case-notes-01/README.md`
   - Focus: structured case notes, observables, tasking, and incident documentation workflow

4) **Trojanized Productivity App Download — Alert Triage & Escalation**
   - Path: `projects/trojan-app-triage-01/README.md`
   - Includes: triage note, escalation summary, IOC tracking, and Wireshark investigation notes

## Templates
Reusable SOC documentation templates are under `templates/`.

## Data Handling Note
All content is lab-based and sanitized. Identifiers (domains, IPs, usernames, hostnames, timestamps) are redacted or replaced with representative values. No proprietary or sensitive customer/employer data is included.
