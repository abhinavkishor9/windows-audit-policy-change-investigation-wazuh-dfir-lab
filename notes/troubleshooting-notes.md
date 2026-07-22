# Troubleshooting Notes

## Issue 1 — Event ID 4719 Not Generated

### Cause

Required audit policy was not enabled.

### Resolution

Enabled Audit Policy Change auditing using:

```
auditpol /set /subcategory:"Other Policy Change Events" /success:enable
```

---

## Issue 2 — Event Not Visible in Event Viewer

### Cause

Incorrect audit configuration.

### Resolution

Verified settings using:

```
auditpol /get /category:*
```

---

## Issue 3 — Event Missing in Wazuh

### Cause

Initially suspected EventChannel collection or forwarding issue.

### Resolution

Validated:

- Agent running
- Agent connected
- EventChannel configured
- alerts.json

---

## Issue 4 — No Results in Discover

### Cause

Time filter excluded newly generated events.

### Resolution

Expanded the Discover time range and refreshed the index.

---

## Issue 5 — Agent Appeared Offline

### Observation

Agent log showed temporary disconnections.

### Resolution

Confirmed reconnection using:

```
agent_control -i 001
```

Status returned:

```
Active
```

---

## Issue 6 — Verify Event Collection

Validated using:

```
grep '"eventID":"4719"' alerts.json
```

Result

Successful ingestion confirmed.

---

# Lessons Learned

- Always validate events locally before troubleshooting Wazuh.
- PowerShell provides an excellent secondary validation method.
- alerts.json is the most reliable source to verify manager ingestion.
- Discover confirms successful indexing and parsing.
- Agent connectivity should always be verified before investigating missing events.
