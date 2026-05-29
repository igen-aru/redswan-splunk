# Attack Plan

## Purpose

This plan defines safe, controlled attack simulations for generating telemetry used in the lab.

## Rules of Engagement

- Use only isolated lab systems.
- Use benign commands and payloads.
- Do not run unauthorized tests against real environments.
- Record timestamps of all tests for easier Splunk validation.

## Scenario 1: Suspicious PowerShell

### Goal
Generate PowerShell execution logs that resemble malicious tradecraft.

### Actions
- Launch PowerShell with `-enc`
- Run a harmless encoded command
- Execute from a non-admin user context if possible
- Ensure PowerShell Script Block Logging is enabled

### Expected Data
- EventCode 4104
- Process creation events
- command line containing encoded or hidden execution flags

## Scenario 2: SSH Brute Force

### Goal
Generate repeated failed SSH logins from one source IP.

### Actions
- Attempt several failed SSH logins against a lab Linux host
- Optionally follow with one successful login
- Capture auth.log or equivalent syslog source

### Expected Data
- repeated `Failed password` events
- source IP, username, hostname
- optional success after failures

## Scenario 3: Lateral Movement

### Goal
Generate Windows telemetry consistent with credential-based remote movement.

### Actions
- Use a lab account to trigger explicit credential usage
- Generate remote access or administrative logon behavior
- Record associated process creation where available

### Expected Data
- EventCode 4648
- EventCode 4624 with relevant LogonType values
- EventCode 4688 for spawned processes

## Lab Validation

After each scenario:
1. confirm data arrived in Splunk
2. verify timestamps
3. test SPL detection
4. record screenshots and findings
