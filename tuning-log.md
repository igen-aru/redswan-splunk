# Tuning Log

## Purpose

This log records tuning decisions for the detections in this project.

---

## Detection: suspicious-powershell.spl

### Initial Logic
Scored PowerShell activity using encoded command, hidden window, execution policy bypass, and download-related indicators.

### Observed Noise
- legitimate admin scripts
- software deployment tooling
- automation frameworks using PowerShell

### Tuning Decisions
- required a minimum score threshold
- preserved medium severity for lower-confidence cases
- recommended future allowlists for known admin hosts

### Next Improvements
- incorporate parent-child process relationships
- add allowlists for management platforms
- enrich with network telemetry

---

## Detection: brute-force-ssh.spl

### Initial Logic
Flagged five or more failed SSH logins from one source within ten minutes.

### Observed Noise
- vulnerability scanners
- misconfigured automation
- users with stale credentials

### Tuning Decisions
- retained threshold of 5 for lab visibility
- added severity scaling by count
- recommended exclusions for known scanners

### Next Improvements
- correlate with successful login after failures
- track target host concentration
- add geo or asset enrichment

---

## Detection: lateral-movement.spl

### Initial Logic
Combined explicit credentials, remote logon activity, and suspicious admin tooling.

### Observed Noise
- help desk activity
- administrative remote access
- jump-box operations

### Tuning Decisions
- required suspicious score >= 2
- grouped by source and account for easier triage
- preserved command and process context

### Next Improvements
- enrich with asset criticality
- include privileged account tagging
- model risk-based alerting fields
