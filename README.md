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
cmd.exe / c whoami
```
**Notepad.exe OR Calc.exe OR whoami**
<img width="886" height="114" alt="image" src="https://github.com/user-attachments/assets/fbca3a47-e61e-483d-a988-2676d66156f9" />


### Splunk Investigation

```spl
index=main source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
notepad.exe OR calc.exe OR whoami
```

### Results

**WhoAMI**

<img width="944" height="418" alt="image" src="https://github.com/user-attachments/assets/07963b89-0dcb-45b1-b36e-2babc7cd448c" />

**Notepad.exe & Calc.exe**

<img width="746" height="341" alt="image" src="https://github.com/user-attachments/assets/7f306b86-caa2-4d0c-96b6-9dc8ffadc20c" />

### Findings

The executed processes were successfully identified within Splunk, confirming that Sysmon process creation events were collected and available for threat hunting and incident response workflows.

### MITRE ATT&CK

- T1059.003 Windows Command Shell

---

### Use Case 2: Network Connection Monitoring

A Kali Linux VM was used to simulate an external attacker performing reconnaissance against a Windows 10 endpoint. The objective was to generate network activity that could be investigated within Splunk using Sysmon telemetry.

### Attacker System

| Host | IP Address | Role |
|--------|------------|--------|
| Kali Linux | 10.0.2.15 | Attacker |
| Windows 10 Endpoint | 10.0.2.4 | Target |

### Attack Performed

The following Nmap service discovery scan was executed from the Kali Linux VM:

```bash
nmap -sV 10.0.2.4
```

**Nmap**

<img width="1269" height="637" alt="image" src="https://github.com/user-attachments/assets/83c31dd7-c98d-4363-9a0a-4822c84727b9" />


### Expected Outcome

The scan generates reconnaissance activity against the Windows endpoint that can be investigated within Splunk.

### Splunk Investigation

Search:

```spl
index=main "10.0.2.15"
```
**Splunk**

<img width="1888" height="822" alt="image" src="https://github.com/user-attachments/assets/088dadd1-b6dd-458d-95ac-6c2031ce8f6b" />


### Findings

Splunk returned events containing the Kali Linux IP address (`10.0.2.15`), demonstrating visibility into activity originating from the simulated attacker machine.

### MITRE ATT&CK Mapping

 T1046 - Network Service Discovery

---

### Use Case 3: DNS Query Monitoring

### Use Case 4: PowerShell Execution Detection

### Use Case 5: Encoded PowerShell Detection
