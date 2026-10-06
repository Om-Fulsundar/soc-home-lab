INVESTIGATION REPORT
====================
Alert ID: IR‑2026‑001

Date: 2026‑10‑03

Analyst: Om Fulsundar

Severity: MEDIUM

Status: CLOSED - TRUE POSITIVE

ALERT DETAILS
-------------
Source: Wazuh + Splunk

Rule: Authentication_Failures

Event ID: 4625

ATTACK SUMMARY
--------------
10 failed login attempts generated from
local machine (::1) targeting account “gr0ot”
to simulate brute force attack.
All attempts detected by Wazuh and Splunk.

TIMELINE
--------
[20:30] Brute force PowerShell script run

[20:31] Wazuh alert triggered - 4625 ×10

[21:28] Splunk BruteForce‑Detection fired

[21:35] Investigation complete

EVIDENCE
--------
Event ID: 4625
Log Source: Windows Security Log

SIEM: Wazuh - Authentication_Failures rule

Splunk: BruteForce‑Detection report

Screenshot: simulations/brute‑force/

MITRE ATT&CK
-----------
Tactic: Credential Access

Technique: T1110 - Brute Force

Sub‑technique: T1110.001 - Password Guessing

VERDICT
-------
TRUE POSITIVE - Simulated brute force

confirmed by both Wazuh and Splunk

SOC RESPONSE
------------
1. Identify source IP - internal (::1)
2. Check if Event 4624 follows the 4625s
   If yes - brute force succeeded
3. Block source IP at firewall
4. Reset password of targeted account
5. Search for lateral movement from that IP
6. Escalate if production account targeted

RECOMMENDATIONS
---------------
1. Implement account lockout after 5 failures
2. Enable MFA on all privileged accounts
3. Create SIEM alert for >3 failures in 60 s
