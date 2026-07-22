# windows-audit-policy-change-investigation-wazuh-dfir-lab
## Overview

This DFIR lab demonstrates how Windows Audit Policy Change events (Event ID 4719) can be generated, collected, forwarded, and investigated using Wazuh.

Unlike simple event viewing exercises, this investigation validates the complete telemetry pipeline—from Windows Event Viewer to the Wazuh agent, manager, alerts.json, and Wazuh Discover.

---

# Executive Summary

During this investigation, Windows Audit Policy settings were modified to intentionally generate Event ID 4719. The generated event was validated locally using Event Viewer and PowerShell before confirming successful ingestion into Wazuh.

The investigation also involved troubleshooting missing telemetry, verifying agent connectivity, confirming event forwarding, and validating alert generation using alerts.json and Wazuh Discover.

---

# Learning Objectives

- Understand Windows Audit Policy Change events.
- Generate Event ID 4719.
- Verify Windows Security logging.
- Validate Wazuh agent connectivity.
- Confirm event forwarding.
- Investigate alerts using Wazuh Discover.
- Validate collected evidence using alerts.json.
- Correlate multiple forensic artifacts.

---

# Skills Demonstrated

- Windows DFIR Investigation
- Windows Security Event Analysis
- Event ID 4719 Investigation
- Windows Audit Policy Analysis
- Wazuh Agent Validation
- Wazuh Log Collection
- JSON Alert Analysis
- Evidence Correlation
- Event Pipeline Validation
- DFIR Documentation
- Troubleshooting Telemetry Issues

---

# Tools Used

- Windows Event Viewer
- PowerShell
- auditpol.exe
- Wazuh Agent
- Wazuh Manager
- Wazuh Discover
- alerts.json
- Linux Terminal

---

# Lab Environment

| Component | Details |
|------------|---------|
| Operating System | Windows 11 Pro |
| SIEM | Wazuh 4.12 |
| Investigation Type | Windows DFIR |
| Event Source | Windows Security Log |
| Event ID | 4719 |
| Log Collection | EventChannel |

---

# Investigation Scenario

A security administrator suspects that Windows auditing has been modified on an endpoint.

As the DFIR analyst, your objectives are to:

- Generate an Audit Policy Change event
- Verify local logging
- Validate Wazuh agent connectivity
- Confirm event ingestion
- Correlate evidence across multiple sources
- Verify successful alert generation

---

# Investigation Workflow

1. Verify Wazuh agent status.
2. Review current Windows audit policy.
3. Modify Audit Policy settings.
4. Generate Event ID 4719.
5. Verify Event Viewer.
6. Validate using PowerShell.
7. Confirm Wazuh agent connectivity.
8. Validate event in alerts.json.
9. Investigate event in Wazuh Discover.
10. Correlate evidence.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Defense Evasion | Modify Authentication Process | T1556 |
| Defense Evasion | Indicator Removal / Logging Modification | T1070 |

---

# Why Event ID 4719 Matters

Event ID 4719 records changes to Windows auditing policies.

Threat actors frequently modify auditing to reduce logging visibility before carrying out malicious actions. Monitoring this event provides defenders with early visibility into potential attempts to weaken endpoint logging.

---

# Evidence Collected

- Windows Audit Policy
- Event Viewer (4719)
- PowerShell verification
- Wazuh agent status
- alerts.json
- Wazuh Discover event
- Linux manager validation

---

# Evidence Correlation

| Evidence Source | Information Obtained | Investigation Value |
|-----------------|---------------------|--------------------|
| auditpol | Audit configuration | Baseline |
| Event Viewer | Event ID 4719 | Local validation |
| PowerShell | Event verification | Independent validation |
| Agent Control | Agent connectivity | Pipeline validation |
| alerts.json | Raw event | Manager confirmation |
| Wazuh Discover | Parsed event | SIEM validation |

---

# Investigation Findings

- Audit Policy changes successfully generated Event ID 4719.
- Windows Security Log captured the event.
- PowerShell confirmed successful logging.
- Wazuh agent remained connected.
- alerts.json confirmed event ingestion.
- Wazuh Discover successfully parsed the event.
- Evidence was successfully correlated across all forensic sources.

---

# Key Takeaways

- Event ID 4719 provides visibility into audit policy modifications.
- Multiple evidence sources should always be correlated.
- Wazuh Discover validates successful parsing.
- alerts.json confirms manager ingestion.
- Agent connectivity is essential for reliable telemetry.
- Native Windows tools complement SIEM investigations.

---

