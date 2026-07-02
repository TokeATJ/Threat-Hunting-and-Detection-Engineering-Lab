# Detection-Engineering-Lab

## Detection Engineering Lab

**Confirm Data Source**

```spl
index=main
| stats count by source
```
You should see log sources similar to the following:

| Source | Description |
|----------|-------------|
| WinEventLog:Application | Windows Application Logs |
| WinEventLog:Security | Windows Security Logs |
| WinEventLog:System | Windows System Logs |
| WinEventLog:Microsoft-Windows-Sysmon/Operational | Sysmon Telemetry |

<img width="1405" height="694" alt="image" src="https://github.com/user-attachments/assets/94584eef-1d62-4c83-99d7-dc7faee2b45e" />

### Use Case 1: Process Creation Monitoring

### Use Case 2: Network Connection Monitoring

### Use Case 3: DNS Query Monitoring

### Use Case 4: PowerShell Execution Detection

### Use Case 5: Encoded PowerShell Detection
