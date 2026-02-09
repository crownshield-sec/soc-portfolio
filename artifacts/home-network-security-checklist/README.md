# Home Network Security Checklist (SOC L1 Evidence Pack)
## Environment (Home Setup)
- ISP gateway: Spectrum-provided router/gateway (primary routing, NAT/DHCP, WAN-facing controls)
- Wireless access point: TP-Link Archer A8 in Access Point (AP) mode (Wi-Fi security and guest wireless where supported)
- Note: Some router security controls and logs are limited or not exposed in ISP-managed interfaces; evidence is captured where settings are available.

## Objective
Implement and verify baseline router and Wi-Fi hardening controls that reduce common home-network attack paths (exposed management, unsafe defaults, weak wireless security, unnecessary inbound exposure) and document evidence in an analyst-ready format.

## Scope
**In scope:** router administrative security, WAN exposure controls, Wi-Fi security baseline, guest/IoT segmentation (as supported), DNS configuration (as applicable), and basic logging/visibility.  
**Out of scope:** endpoint EDR, enterprise SIEM ingestion, vulnerability scanning beyond router firmware, and advanced IDS/IPS tuning.

## Control Checklist (Implementation + Verification)

### A) Administrative Hardening (Control Plane)
- [ ] Admin password updated (strong + unique)
- [ ] Remote administration disabled (WAN-side management OFF)
- [ ] Firmware updated (or update plan documented)
- [ ] Time/NTP configured correctly (log integrity)
- [ ] Configuration backup created and stored securely

### B) Reduce External Exposure (Attack Surface)
- [ ] UPnP disabled (or exception documented)
- [ ] Port forwarding reviewed; unnecessary rules removed
- [ ] WPS disabled
- [ ] Firewall enabled; inbound deny-by-default confirmed

### C) Wi-Fi Security Baseline
- [ ] WPA3-Personal enabled (or WPA2-AES fallback documented)
- [ ] Strong passphrase configured
- [ ] Guest network enabled and isolated from LAN
- [ ] IoT segmented (separate SSID/VLAN/guest-based isolation if supported)

### D) DNS / Basic Threat Reduction (Optional by Router Capability)
- [ ] DNS set to a reputable resolver (documented)
- [ ] If supported: encrypted DNS (DoH/DoT) enabled
- [ ] If supported: malicious domain blocking / security DNS feature enabled

### E) Observability (SOC Mindset)
- [ ] Router logging enabled (as supported)
- [ ] Logging limitations documented (retention, event types)
- [ ] If supported: syslog/export configured (optional)

## Validation Tests Performed
- Guest isolation test: guest device cannot reach LAN IPs/admin console (as configured)
- UPnP status verified OFF
- Firewall / inbound deny setting verified in router UI
- Firmware version/date captured as evidence

## Evidence Appendix (Sanitized)
Status: **Pending upload** — screenshots will be added after sanitization and redaction.

Planned evidence files (to be uploaded into `images/`):
- `images/01_remote_admin_off.png`
- `images/02_firmware_version.png`
- `images/03_upnp_off.png`
- `images/04_port_forwarding.png`
- `images/05_wifi_security_mode.png`
- `images/06_wps_off.png`
- `images/07_guest_isolation.png`
- `images/08_logging.png`

