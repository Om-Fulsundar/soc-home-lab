INVESTIGATION REPORT
====================
Alert ID: IR‑2026‑004
Date: 2026‑10‑05
Analyst: Om Fulsundar
Severity: MEDIUM
Status: CLOSED — TRUE POSITIVE

ALERT DETAILS
-------------
Source: Sysmon + Wazuh
Rule: Outbound SMB Anomalous Connections
Event ID: 3

ATTACK SUMMARY
--------------
Outbound TCP connections detected from
`C:\Program Files (x86)\Nmap\nmap.exe`
on host 127.0.0.1. Activity corresponds to
an internal port‑scan simulation using Nmap
(`nmap ‑sV ‑p 1‑1000 127.0.0.1`).

TIMELINE
--------
[11:10] Nmap scan initiated locally  
[11:10] Sysmon Event ID 3 logged — NetworkConnect  
[11:11] Wazuh alert generated — Outbound SMB connections  
[11:20] Investigation complete

EVIDENCE
--------
Process Image: C:\Program Files (x86)\Nmap\nmap.exe  
User: GROOT\gr00t  
Protocol: TCP  
Source IP: 127.0.0.1  
Source Port: 965  
Rule Name: Outbound SMB Anomalous Connections  
Screenshot: simulations/port‑scan/

MITRE ATT&CK
-----------
Tactic: Discovery  
Technique: T1046 — Network Service Scanning

VERDICT
-------
TRUE POSITIVE — Simulated internal port scan
confirmed by Sysmon and Wazuh logs

SOC RESPONSE
------------
1. Validate source host and user context  
2. Confirm scan scope and target range  
3. Ensure no external IP targets were included  
4. Review firewall logs for related traffic  
5. Escalate if scan originates from production system

RECOMMENDATIONS
---------------
1. Restrict Nmap usage to authorized security accounts  
2. Enable Sysmon network logging for all hosts  
3. Create SIEM alert for >50 unique ports scanned in 60 s
