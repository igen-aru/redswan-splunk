# Data Flow

## Purpose

This document describes how data moves through the Splunk Detection Lab.

## Pipeline

1. Attack simulation generates host, authentication, and process events.
2. Logs are forwarded into Splunk indexes.
3. SPL detections search normalized events.
4. Detection results feed dashboard panels and analyst review.
5. Analysts validate, tune, and document findings.
6. Detection metadata is mapped to MITRE ATT&CK.

## Data Sources

### Windows Security Logs
Relevant event IDs include:
- 4624: successful logon
- 4625: failed logon
- 4648: logon with explicit credentials
- 4688: process creation

### PowerShell Logs
- 4104: script block logging

### Linux Authentication Logs
- `sshd` failed password attempts
- successful SSH logins

### Optional Enrichment
- Sysmon process and network data
- Zeek or firewall logs
- asset and identity lookups

## Suggested Splunk Index Strategy

- `index=windows`
- `index=linux`
- `index=network`

## Search-Time Assumptions

Expected fields may include:
- `_time`
- `host`
- `user`
- `src_ip`
- `dest`
- `CommandLine`
- `ParentCommandLine`
- `EventCode`
- `LogonType`
- `process_name`

## Detection Flow

### Suspicious PowerShell
Windows host events -> PowerShell script logging -> encoded-command detection -> analyst review

### Brute-force SSH
Linux auth logs -> repeated failed logins grouped by source/user -> threshold -> analyst review

### Lateral Movement
Windows credential usage and logon events -> explicit credential use and remote logon indicators -> correlation -> analyst review

## Outputs

- SPL detections
- ATT&CK mapping JSON
- dashboard XML
- case report markdown
- tuning log
