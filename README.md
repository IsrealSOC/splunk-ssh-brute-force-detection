# SSH Brute Force Detection – Splunk SOC Lab

## Objective
Detect SSH brute force attempts using Linux journalctl authentication logs ingested into Splunk.

## Environment
- Linux (journalctl / systemd)
- Splunk Enterprise
- Home SOC Lab
- SSH enabled host

## Data Source
- journalctl logs
- Authentication events (failed SSH logins)

## Detection Logic
- Identify repeated failed SSH login attempts
- Aggregate by source IP and username
- Threshold-based alerting

## Splunk Search
```spl
index=main sourcetype=linux:journald "Failed password"
| stats count by src_ip user
| where count > 5
