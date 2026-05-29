# Detection Tests

## Purpose

These tests help validate that each detection works as expected in a lab environment.

## General Validation Checklist

- Confirm the target index contains relevant events.
- Confirm expected sourcetypes are available.
- Confirm field names match your environment.
- Confirm the query returns results during the expected test window.
- Confirm thresholds are not too low or too high.

## Test 1 - Suspicious PowerShell

### Expected Inputs
- Windows events with EventCode 4104 or 4688
- PowerShell command lines or script blocks

### Validation Steps
1. Run the detection for the last 24 hours.
2. Verify the fields `_time`, `host`, `user`, `process_name`, and `raw_cmd` appear.
3. Trigger a known-safe encoded PowerShell test in the lab.
4. Confirm `suspicious_score` increases correctly.
5. Check for false positives from administration tooling.

### Pass Criteria
- Query returns expected test activity.
- Encoded or hidden execution is visible.
- Noise is reviewable and not overwhelming.

## Test 2 - Brute-force SSH

### Expected Inputs
- Linux auth logs containing `Failed password`
- Source IP and username visible in raw logs

### Validation Steps
1. Trigger at least five failed SSH attempts within ten minutes.
2. Run the query.
3. Confirm source IP grouping is correct.
4. Confirm thresholding works.
5. Confirm internal scanners or monitoring systems are excluded if needed.

### Pass Criteria
- Repeated failed login activity is detected.
- Counts reflect the simulation volume.
- Severity values match threshold logic.

## Test 3 - Lateral Movement

### Expected Inputs
- Windows Security events 4624, 4648, 4688
- Authentication and process context

### Validation Steps
1. Generate a lab event with explicit credentials.
2. Generate a qualifying remote logon where possible.
3. Run the detection.
4. Verify the account and source values correlate correctly.
5. Review whether benign admin activity causes noise.

### Pass Criteria
- Explicit credential use contributes to the score.
- Related remote access behavior is visible.
- The detection returns a manageable number of candidates.

## Field Mapping Notes

Different labs may use different field extractions. If needed, normalize:
- `Account_Name` vs `TargetUserName`
- `Source_Network_Address` vs `IpAddress`
- `CommandLine` vs `Process_Command_Line`

## Known Tuning Areas

- service accounts
- jump hosts
- admin automation
- vulnerability scanners
- backup systems
