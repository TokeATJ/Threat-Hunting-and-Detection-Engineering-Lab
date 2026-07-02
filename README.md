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

### Objective

Validate that Sysmon captures process creation activity and forwards telemetry to Splunk for centralized monitoring and investigation.

### Test Activity

The following processes were executed on the Windows endpoint:

```cmd
notepad.exe
calc.exe
```
<img width="1996" height="439" alt="image" src="https://github.com/user-attachments/assets/2b18a389-f1f6-4ad6-879d-d2f7ec304768" />


### Splunk Investigation

```spl
index=main source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
notepad.exe OR calc.exe 
```

### Results

<img width="931" height="425" alt="image" src="https://github.com/user-attachments/assets/f9e09b34-337a-466d-99db-4b3a32618d43" />

The executed processes were successfully identified within Splunk, confirming that Sysmon process creation events were collected and available for threat hunting and incident response workflows.

### MITRE ATT&CK

- T1059.001 – PowerShell
- T1059.003 – Windows Command Shell

### Use Case 2: Network Connection Monitoring

### Use Case 3: DNS Query Monitoring

### Use Case 4: PowerShell Execution Detection

### Use Case 5: Encoded PowerShell Detection
