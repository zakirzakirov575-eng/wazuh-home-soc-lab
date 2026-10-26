# Installation and Configuration Notes

This document summarizes the setup completed for this lab. It is intentionally a high-level reproducible checklist rather than a dump of machine-specific configuration or secrets.

## 1. Prepare the virtual machine
1. Create an Ubuntu Linux VM in Oracle VirtualBox.
2. Allocate enough RAM, CPU, and disk for the Wazuh components; monitor disk usage during installation.
3. Configure networking so the Windows host can reach the services needed for the lab.
4. Keep the dashboard restricted to local/lab access.

The installer reported that the operating system was not on its recommended list during this setup. Treat compatibility warnings seriously and consult the official Wazuh installation documentation before reproducing on another Ubuntu release.

## 2. Install Wazuh
- The Wazuh installation assistant for version **4.14.9** was used.
- The dashboard service became active and the dashboard login page was reachable over local HTTPS.
- The browser displayed a certificate-authority warning because the lab uses a certificate not trusted by the browser. This is expected for a self-signed/local lab certificate, but it should not be normalized for production.

For current installation steps, use the official [Wazuh documentation](https://documentation.wazuh.com/current/).

## 3. Connect the Windows agent
1. Install the Wazuh agent on the Windows endpoint.
2. Configure the manager address using the actual address reachable from the endpoint.
3. Start the agent service and verify that the endpoint appears as **Active** in the dashboard.
4. Keep agent keys and enrollment secrets out of Git.

The connected endpoint was displayed as `Windows-Host`, with agent ID `001`, and its status was **Active** during verification.

## 4. Configure event collection
The Windows agent configuration file used was:

`C:\\Program Files (x86)\\ossec-agent\\ossec.conf`

Configured event sources included Windows Application, Security, and System logs, plus `Microsoft-Windows-Sysmon/Operational`.

The lab also enabled successful process-creation auditing on Windows and installed/runs Sysmon. Event channel names and audit-policy subcategory names can differ by Windows language and edition.

## 5. Configure file integrity monitoring
A dedicated test directory was configured under the existing Wazuh `syscheck` configuration:

`C:\\SOC-Lab`

The directory was monitored in real time. A test file was modified and another file was created; Wazuh generated the expected integrity alerts.

When editing `ossec.conf`, add new directory settings inside the existing `syscheck` block rather than creating duplicate top-level blocks. Validate XML structure and restart the agent after configuration changes.

## 6. Validate the deployment
- Confirm the agent is **Active**.
- Search for Windows Event ID 4625.
- Confirm Sysmon events arrive from the expected channel.
- Modify and create a test file under `C:\\SOC-Lab` and check the FIM alerts.
- Review vulnerability findings without treating a finding as evidence of compromise.

## Troubleshooting notes
- A browser certificate warning is common with a self-signed lab certificate.
- An active dashboard does not guarantee every backend service or API is healthy; inspect service status and logs if the dashboard reports API or data problems.
- Vulnerability-feed updates and indexer startup can take time.
- Avoid exposing the dashboard directly to the internet.
