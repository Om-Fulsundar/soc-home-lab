INVESTIGATION REPORT
====================
Alert ID: IR‑2026‑002
Date: 2026‑10‑03
Analyst: Om Fulsundar
Severity: MEDIUM
Status: CLOSED — TRUE POSITIVE

ALERT DETAILS
-------------
Source: Wazuh
Rule: Suspicious_Process_Execution
Event ID: N/A (Sysmon/Windows Command Processor)

ATTACK SUMMARY
--------------
Suspicious command execution detected on host
192.168.6.1 (windows‑host). The process
`cmd.exe` launched with parameters:
`/c whoami && ipconfig`, indicating possible
enumeration activity. Logged by Wazuh agent.

TIMELINE
--------
[22:27] Command executed via PowerShell
[22:28] Wazuh alert generated — cmd.exe spawn
[22:29] Log indexed under wazuh‑alerts‑4.x‑2026.10.03
[22:35] Investigation complete

EVIDENCE
--------
Agent ID: 001
Agent IP: 192.168.6.1
Agent Name: windows‑host
Command Line: "C:\Windows\System32\cmd.exe /c whoami && ipconfig"
Company: Microsoft Corporation
Integrity Level: High
Hashes: SHA1=D1682AE6D9EEC5C9856084B022F1AF696EAD9A9
Image Path: C:\Windows\System32\cmd.exe
Screenshot: simulations/suspicious‑process/

MITRE ATT&CK
-----------
Tactic: Discovery
Technique: T1059 — Command and Scripting Interpreter
Sub‑technique: T1059.003 — Windows Command Shell

VERDICT
-------
TRUE POSITIVE — Simulated process execution
confirmed by Wazuh agent logs

SOC RESPONSE
------------
1. Verify parent process and user context
2. Check for subsequent network or registry activity
3. Review PowerShell history for related commands
4. Confirm if cmd.exe was invoked by legitimate admin
5. Escalate if persistence or privilege escalation observed

RECOMMENDATIONS
---------------
1. Restrict PowerShell and cmd usage to admins only
2. Enable command‑line logging and script block auditing
3. Create SIEM alert for cmd.exe with enumeration keywords
