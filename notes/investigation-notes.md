# Investigation Notes

## Lab Summary

This investigation validated the complete lifecycle of Windows Audit Policy Change events using Wazuh.

Rather than only generating Event ID 4719, the investigation confirmed successful event collection across every stage of the telemetry pipeline.

---

## Analyst Methodology

The investigation followed a structured workflow:

1. Verify Wazuh agent status.
2. Review current audit configuration.
3. Modify audit policy.
4. Generate Event ID 4719.
5. Validate Event Viewer.
6. Verify using PowerShell.
7. Confirm agent connectivity.
8. Validate alerts.json.
9. Investigate event inside Wazuh Discover.
10. Correlate all collected evidence.

---

## Investigation Scenario

An administrator suspects that Windows auditing has been modified.

Objectives:

- Verify auditing changes
- Confirm Windows logging
- Validate SIEM ingestion
- Correlate forensic artifacts

---

## Evidence Collected

### Evidence 1 — Windows Audit Policy

Command

```
auditpol /get /category:*
```

Finding

Verified current auditing configuration.

---

### Evidence 2 — Audit Policy Modification

Command

```
auditpol /set /subcategory:"Other Policy Change Events" /success:disable

auditpol /set /subcategory:"Other Policy Change Events" /success:enable
```

Finding

Generated Event ID 4719.

---

### Evidence 3 — Event Viewer

Collected:

- Event ID 4719
- Audit Policy Change
- User Account
- Timestamp

Finding

Confirmed Windows recorded the policy modification.

---

### Evidence 4 — PowerShell Validation

Command

```
Get-WinEvent -FilterHashtable @{
 LogName='Security'
 Id=4719
} -MaxEvents 5
```

Finding

Verified Event Viewer results independently.

---

### Evidence 5 — Wazuh Agent Validation

Command

```
sudo /var/ossec/bin/agent_control -i 001
```

Finding

Agent remained connected and synchronized.

---

### Evidence 6 — alerts.json

Command

```
grep '"eventID":"4719"' /var/ossec/logs/alerts/alerts.json
```

Finding

Confirmed successful event ingestion.

---

### Evidence 7 — Wazuh Discover

Collected:

- Rule ID 60112
- Event ID 4719
- Agent Name
- Audit Policy details
- EventChannel decoder

Finding

Validated complete parsing inside Wazuh.

---

## DFIR Analysis

Evidence confirmed:

- Windows generated the event.
- Windows stored the event.
- Wazuh collected the event.
- Manager received the event.
- Discover parsed the event.

Every stage of the telemetry pipeline was successfully validated.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Defense Evasion | Modify Authentication Process | T1556 |
| Defense Evasion | Indicator Removal | T1070 |

---

## Analyst Observations

- Event ID 4719 provides valuable visibility into audit policy modifications.
- Native Windows tools successfully validated event generation.
- alerts.json proved manager ingestion.
- Wazuh Discover confirmed successful event parsing.
- Initial telemetry issues were resolved through systematic troubleshooting.

---

## Conclusion

This investigation demonstrated an end-to-end validation of Windows Security Event 4719 collection using Wazuh, providing confidence that endpoint telemetry is successfully reaching the SIEM.
