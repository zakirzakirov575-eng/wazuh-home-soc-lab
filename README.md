# Wazuh Home SOC Lab

A hands-on home Security Operations Center (SOC) lab built to practice endpoint monitoring, centralized log analysis, file integrity monitoring (FIM), Windows event investigation, Sysmon telemetry, and vulnerability detection.

**Status:** Core lab is operational. Results below describe events observed in this lab; they are not claims of a production deployment or proof that a host was compromised.

## Goals
- Deploy Wazuh on an Ubuntu virtual machine.
- Connect a Windows 11 endpoint using the Wazuh agent.
- Collect Windows Security, System, Application, and Sysmon logs.
- Detect file changes in a dedicated test directory.
- Hunt for failed Windows logons.
- Review vulnerability-detection findings and interpret alerts carefully.

## Architecture
- **Host:** Windows 11
- **Virtualization:** Oracle VirtualBox
- **SIEM / manager:** Wazuh 4.14.9 on Ubuntu Linux
- **Endpoint:** Windows host with Wazuh agent and Sysmon
- **Dashboard:** Wazuh web interface, accessed locally through VirtualBox port forwarding

See [architecture](docs/architecture.md) and [installation notes](docs/installation.md).

## Verified scenarios

| Scenario | Evidence observed | Result |
|---|---|---|
| File modified | Wazuh rule **550**, level **7**, integrity checksum changed | Detected |
| New file created | Wazuh rule **554**, level **5**, file added to the system | Detected |
| Failed Windows logons | Event ID **4625**, Wazuh rule **60122** | Events searchable |
| Sysmon telemetry | Sysmon Operational events ingested | Collection confirmed |
| Vulnerability detection | VirtualBox-related CVE findings shown in dashboard | Findings available for triage |

Detailed evidence and limitations: [detection scenarios](docs/detection-scenarios.md) and [sample incident notes](docs/incident-report.md).

## Evidence screenshots

Sanitized screenshots from the lab are available here:

1. [Windows agent active](screenshots/wazuh-agent-active.png.png)
2. [FIM: file modified — rule 550](screenshots/fim-file-modified.png)
3. [FIM: file added — rule 554](screenshots/fim-file-added.png)
4. [Failed Windows logons — Event ID 4625](screenshots/failed-logons-4625.png)
5. [Vulnerability Detection finding](screenshots/vulnerability-detection.png)

The screenshots document observed lab behavior. They do not, by themselves, demonstrate exploitation or a production security incident.

## Hunting queries
Example Wazuh Discover filters are documented in [queries/wazuh-hunting.md](queries/wazuh-hunting.md).

## Security and privacy
- Do **not** commit passwords, API keys, agent keys, private IP details, screenshots containing secrets, or raw logs with personal information.
- Dashboard addresses in this project are examples for local use only. Do not expose the dashboard publicly.
- A vulnerability finding is not proof of exploitation or compromise.
- A single failed logon is not enough to conclude that an attack occurred. Correlate with account, process, source, time, and surrounding events.

## Next steps
- Build a controlled detection test for additional Windows events.
- Document triage steps and false-positive considerations for each alert.
- Add a small incident timeline based on correlated events.

## Skills practiced
Wazuh SIEM, Linux administration, Windows event logs, Sysmon, file integrity monitoring, event search, vulnerability triage, MITRE ATT&CK context, and concise incident documentation.
