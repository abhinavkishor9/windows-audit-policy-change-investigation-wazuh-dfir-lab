# Investigation Timeline

| Time | Activity | Evidence |
|------|----------|----------|
| 07:20 | Verified Wazuh agent connectivity | agent_control |
| 07:24 | Reviewed current audit configuration | auditpol |
| 07:30 | Modified Audit Policy | auditpol |
| 07:31 | Generated Event ID 4719 | Windows Security Log |
| 07:33 | Verified Event Viewer | Event ID 4719 |
| 07:34 | Verified using PowerShell | Get-WinEvent |
| 07:36 | Validated alerts.json | grep eventID 4719 |
| 07:38 | Investigated event in Wazuh Discover | Rule 60112 |
| 07:42 | Correlated evidence | Documentation |
| 07:45 | Investigation completed | Final findings |

---

# Investigation Flow

```
Verify Agent
      ↓
Review Audit Policy
      ↓
Modify Policy
      ↓
Generate Event 4719
      ↓
Verify Event Viewer
      ↓
Validate PowerShell
      ↓
Check alerts.json
      ↓
Investigate in Discover
      ↓
Correlate Evidence
      ↓
Investigation Complete
```

---

# Summary

This investigation successfully validated the complete Windows Security Event 4719 telemetry pipeline. Audit policy modifications were generated, verified locally, forwarded by the Wazuh agent, received by the manager, confirmed in `alerts.json`, parsed by Wazuh Discover, and correlated into a structured DFIR investigation.
