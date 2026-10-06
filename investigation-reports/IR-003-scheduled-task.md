INVESTIGATION REPORT
====================

Alert ID: IR‑2026‑003

Date: 2026‑10‑03

Analyst: Om Fulsundar

Severity: MEDIUM

Status: CLOSED - TRUE POSITIVE

ALERT DETAILS
-------------
Source: Wazuh

Rule: Scheduled_Task_Creation

Event ID: N/A (Sysmon/Windows Task Scheduler)

ATTACK SUMMARY
--------------
Suspicious scheduled task created on host
192.168.6.1 (windows‑host) using PowerShell.
The task “WindowsUpdateCache” executes
`powershell.exe -WindowStyle Hidden`, indicating
potential persistence or stealth execution.

TIMELINE
--------
[22:47] PowerShell command executed as Admin

[22:48] schtasks.exe invoked - task created

[22:49] Wazuh alert generated - Scheduled Task/Job

[22:55] Investigation complete

EVIDENCE
--------
Agent ID: 001

Agent IP: 192.168.6.1

Agent Name: windows‑host

Executable: C:\Windows\System32\schtasks.exe

Description: Task Scheduler COM API

Hashes: SHA1=BF09E52372CF6663743A6FC58FCDB75D7551CD64

Rule Name: technique_id=T1053, technique_name=Scheduled Task/Job

Signature: Microsoft Windows - Valid

Screenshot: simulations/scheduled‑task/

MITRE ATT&CK
-----------
Tactic: Persistence

Technique: T1053 - Scheduled Task/Job

Sub‑technique: T1053.005 - Scheduled Task

VERDICT
-------
TRUE POSITIVE - Simulated scheduled task creation
confirmed by Wazuh agent logs

SOC RESPONSE
------------
1. Verify task name and execution path
2. Check if task runs PowerShell or hidden scripts
3. Review creation user and privileges
4. Remove unauthorized scheduled tasks
5. Monitor for repeated task creation attempts

RECOMMENDATIONS
---------------
1. Restrict task creation to administrators only
2. Enable auditing for schtasks.exe and PowerShell
3. Create SIEM alert for hidden PowerShell tasks
