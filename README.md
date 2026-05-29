# redswan-splunk
# Splunk Detection Lab

A detection engineering lab for building, tuning, and documenting Splunk detections for realistic attack scenarios.

## Overview

This project demonstrates an end-to-end SOC workflow:

- Simulate attacker behavior
- Ingest security logs into Splunk
- Write and tune SPL detections
- Map detections to MITRE ATT&CK
- Build a monitoring dashboard
- Produce investigation reports
- Validate repository quality with CI

The repo is inspired by modern Splunk detection engineering practices such as detection lifecycle management, adversary simulation, testing, tuning, and detection-as-code.

## Objectives

- Build practical SPL detections for common attacker behaviors
- Show detection reasoning and tuning decisions
- Create artifacts a SOC team could actually review
- Present a polished GitHub portfolio project for cybersecurity roles

## Detection Scenarios

1. Suspicious PowerShell execution
2. SSH brute-force activity
3. Windows lateral movement with explicit credentials

## Repository Layout

```text
splunk-detection-lab/
├── README.md
├── architecture/
│   └── data-flow.md
├── simulations/
│   ├── attack-plan.md
│   └── data-sources/
│       ├── windows-security-logs/
│       ├── auth-logs/
│       └── network-logs/
├── detections/
│   ├── splunk-spl/
│   │   ├── suspicious-powershell.spl
│   │   ├── brute-force-ssh.spl
│   │   └── lateral-movement.spl
│   ├── sigma/
│   └── mapping/
│       └── attack-to-detection.json
├── dashboards/
│   └── soc-monitoring-dashboard.xml
├── reports/
│   └── case-001-incident-report.md
├── tests/
│   └── detection-tests.md
├── tuning-log.md
└── .github/
    └── workflows/
        └── validate-detections.yml
```

## Prerequisites

- Splunk Enterprise or Splunk Cloud test environment
- Test log data from Windows, Linux auth logs, and optional Sysmon/network telemetry
- Familiarity with SPL and Windows security event IDs

## Suggested Lab Data

- Windows Security Logs: EventCode 4624, 4625, 4648, 4688
- PowerShell logs: EventCode 4104
- Linux auth logs: sshd failed login attempts
- Optional Sysmon and network logs for enrichment

## Detections

### 1. suspicious-powershell.spl
Detects potentially malicious PowerShell execution using encoded commands and suspicious flags.

### 2. brute-force-ssh.spl
Detects repeated failed SSH logins from the same source followed by success.

### 3. lateral-movement.spl
Detects use of explicit credentials and suspicious logon behavior consistent with lateral movement.

## ATT&CK Mapping

Each detection is mapped to one or more MITRE ATT&CK techniques in:

- `detections/mapping/attack-to-detection.json`

## Dashboard

Import `dashboards/soc-monitoring-dashboard.xml` into Splunk as a Simple XML dashboard.

## Testing

Use the tests in `tests/detection-tests.md` to validate:
- expected fields exist
- detections return expected events
- thresholds are reasonable
- false positives are reviewed

## Tuning

Review `tuning-log.md` for threshold rationale and known noise sources.

## Notes

- This repository is for defensive security research and portfolio demonstration.
- Use only authorized lab or simulated data.
- Do not upload malware binaries or sensitive production logs.

## Future Improvements

- Add Sigma parity rules
- Add RBA scoring fields
- Add Attack Range style simulation runs
- Add savedsearches.conf examples
