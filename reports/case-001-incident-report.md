# Case 001 - Suspicious PowerShell Execution

## Summary

A PowerShell detection triggered on a Windows host after command-line activity consistent with encoded execution and possible remote retrieval behavior.

## Alert Source

- Detection: `suspicious-powershell.spl`
- Severity: High
- Index: `windows`

## Key Evidence

- PowerShell-related process observed
- command line included suspicious execution flags
- host generated events indicating script or process activity
- behavior matched the analytic scoring threshold

## Example Investigation Workflow

1. Review the raw command line and process tree.
2. Identify parent process and initiating user.
3. Search for nearby authentication activity from the same host.
4. Search for outbound connections or download indicators.
5. Determine whether execution was administrative, testing-related, or malicious.

## Sample Analyst Notes

The event set suggests suspicious PowerShell usage rather than routine administration because the command line contains indicators commonly associated with defense evasion or scripted execution. If the host belongs to an administrator or lab operator, validate expected activity before escalation.

## Recommended Response

- isolate the host if malicious behavior is confirmed
- collect volatile evidence where appropriate
- reset credentials if compromise is suspected
- review adjacent hosts for similar behavior
- tune allowlists carefully to avoid suppressing real threats

## Final Status

Status: Under investigation

## Lessons Learned

This case demonstrates why process creation data and PowerShell visibility are valuable for high-fidelity detections.
