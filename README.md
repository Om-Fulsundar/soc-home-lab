\# SOC Home Lab — Wazuh + Splunk + Sysmon



\[!\[Platform](https://img.shields.io/badge/Platform-VMware-blue)]()

\[!\[SIEM](https://img.shields.io/badge/SIEM-Wazuh%20%2B%20Splunk-green)]()

\[!\[OS](https://img.shields.io/badge/OS-Windows%20%2B%20Ubuntu-orange)]()



\## Overview

Complete SOC detection environment built locally

on VMware Workstation. Deployed Wazuh as primary

SIEM, Splunk for log analysis and dashboards,

and Sysmon for deep Windows telemetry.

Simulated 4 real-world attack scenarios and

detected every single one.



\## Architecture

!\[Architecture](architecture.png)



\## Lab Components

| Component | Role | Location |

|---|---|---|

| Wazuh Manager 4.9 | SIEM + alerting engine | VMware Ubuntu 22.04 |

| Wazuh Agent | Log collection + shipping | Windows host |

| Splunk Enterprise | Log analysis + dashboards | Windows host |

| Sysmon (olafhartong config) | Deep Windows telemetry | Windows host |



\## Setup Screenshots

| Screenshot | Description |

|---|---|

| \[Wazuh Dashboard](setup/01-wazuh-dashboard.png) | Wazuh manager running |

| \[Agent Connected](setup/02-wazuh-agent-connected.png) | Windows agent active |

| \[Sysmon Running](setup/03-sysmon-running.png) | Sysmon service status |

| \[Splunk Data](setup/05-splunk-data-ingesting.png) | Logs ingesting |

| \[SOC Dashboard](setup/06-splunk-dashboard-final.png) | 5 panel dashboard |



\## Attacks Simulated + Detected

| Attack | MITRE Technique | Event ID | Detected By |

|---|---|---|---|

| Brute Force | T1110 — Brute Force | 4625 | Wazuh + Splunk |

| Suspicious Process | T1059 — Cmd/PS | Sysmon Event 1 | Sysmon + Wazuh |

| Scheduled Task | T1053 — Persistence | Event 4698 | Windows + Wazuh |

| Port Scan | T1046 — Recon | Sysmon Event 3 | Sysmon + Wazuh |



\## Splunk Detection Rules

5 custom SPL queries — \[detection-rules/](detection-rules/)



| Rule | Detects | Event |

|---|---|---|

| brute-force.spl | >5 failed logins same account | 4625 |

| suspicious-process.spl | Unusual process execution | Sysmon 1 |

| network-connections.spl | Outbound connection monitor | Sysmon 3 |

| rare-processes.spl | Anomalous process detection | Sysmon 1 |

| event-volume.spl | Event spike detection | All |



\## Investigation Reports

4 structured IR reports — \[investigation-reports/](investigation-reports/)



| Report | Attack | Verdict |

|---|---|---|

| \[IR-001](investigation-reports/IR-001-brute-force.md) | Brute Force | True Positive |

| \[IR-002](investigation-reports/IR-002-suspicious-process.md) | Suspicious Process | True Positive |

| \[IR-003](investigation-reports/IR-003-scheduled-task.md) | Scheduled Task | True Positive |

| \[IR-004](investigation-reports/IR-004-port-scan.md) | Port Scan | True Positive |



\## Splunk Dashboard

5-panel SOC monitoring dashboard covering

event volume, top event IDs, failed logins,

process creation, and outbound connections.



!\[Dashboard](setup/06-splunk-dashboard-final.png)



\## Key Learnings

\- Sysmon with olafhartong config captures

&#x20; command lines, parent processes, and hashes

&#x20; — dramatically richer than default Windows logs

\- Wazuh out-of-box rules detected all 4

&#x20; simulated attacks without custom tuning

\- Splunk SPL correlation search finds attack

&#x20; chains that individual alerts miss

\- Every simulated attack left detectable

&#x20; artifacts — no attack was invisible

\- Combining two SIEMs gives defense in depth

&#x20; and validates detections independently



\## Tools Used

Wazuh 4.9, Splunk Enterprise, Sysmon,

VMware Workstation 17.5, nmap, Windows

Event Viewer, VirusTotal



\## References

\- MITRE ATT\&CK: attack.mitre.org

\- Sysmon config: github.com/olafhartong/sysmon-modular

\- Wazuh docs: documentation.wazuh.com

