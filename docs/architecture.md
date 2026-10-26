# Lab Architecture

## Components
| Component | Role |
|---|---|
| Windows 11 host | Endpoint being monitored and machine running VirtualBox |
| Oracle VirtualBox | Runs the Linux virtual machine |
| Ubuntu Linux VM | Hosts Wazuh manager, indexer, and dashboard components |
| Wazuh agent for Windows | Forwards endpoint telemetry to the manager |
| Sysmon | Adds detailed Windows process and system activity telemetry |
| Wazuh dashboard | Search, alert review, vulnerability findings, and agent status |

## Data flow
1. Windows generates Security, System, Application, and Sysmon events.
2. The Wazuh agent collects configured event channels and forwards events to the Wazuh manager.
3. Wazuh analyzes events and indexes searchable data.
4. The analyst uses the dashboard to filter events, inspect rule metadata, and investigate findings.

## Network notes
The lab uses VirtualBox NAT with port forwarding to make the dashboard and agent communication available between the host and guest. The dashboard is accessed locally through a forwarded HTTPS port.

Typical Wazuh agent communication uses TCP ports **1514** (agent event traffic) and **1515** (agent enrollment), while the dashboard commonly listens on HTTPS **443** inside the guest. Exact configuration can vary by deployment.

Do not publish actual local IP addresses, private port-forwarding configuration, credentials, or agent keys in public screenshots.

## Scope and limitations
This is a single-endpoint learning lab, not a production SOC. It does not represent high availability, enterprise-scale retention, a full network sensor deployment, or a validated incident-response environment.
