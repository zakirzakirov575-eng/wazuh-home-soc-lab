# Wazuh Home SOC Lab

A small home lab I built to get practical experience with Wazuh and Windows event investigation.

## Setup

- Windows 11 host
- Oracle VirtualBox
- Ubuntu VM running Wazuh 4.14.9
- Wazuh agent and Sysmon on the Windows endpoint

The dashboard is available locally through VirtualBox port forwarding.

## What I tested

| Test | Result |
|---|---|
| Modified a file in `C:\\SOC-Lab` | Wazuh rule 550 fired |
| Created a file in `C:\\SOC-Lab` | Wazuh rule 554 fired |
| Searched Windows failed logons | Found Event ID 4625, Wazuh rule 60122 |
| Checked Sysmon data | Sysmon Operational events appeared in Wazuh |
| Checked vulnerability detection | VirtualBox vulnerability findings appeared in the dashboard |

## Screenshots

- [Windows agent connected](screenshots/wazuh-agent-active.png.png)
- [File modified](screenshots/fim-file-modified.png)
- [File created](screenshots/fim-file-added.png)
- [Failed logons](screenshots/failed-logons-4625.png)
- [Vulnerability finding](screenshots/vulnerability-detection.png)

## Notes

This is a one-endpoint lab, not a production SOC. The failed-logon events and vulnerability findings are examples to investigate, not proof that the machine was attacked. The file changes were made deliberately to test FIM.

More detail:
- [Lab setup](docs/installation.md)
- [Architecture](docs/architecture.md)
- [Detection results](docs/detection-scenarios.md)
- [Triage notes](docs/incident-report.md)
- [Wazuh searches](queries/wazuh-hunting.md)
