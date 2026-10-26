# Lab Architecture

I run Wazuh in an Ubuntu virtual machine on my Windows 11 computer. The Windows host is also the endpoint being monitored.

## Components

| Component | Use |
|---|---|
| Windows 11 | Endpoint and host OS |
| Oracle VirtualBox | Runs the Ubuntu VM |
| Ubuntu + Wazuh 4.14.9 | Manager, indexer, and dashboard |
| Wazuh Windows agent | Sends endpoint events to Wazuh |
| Sysmon | Provides additional Windows activity events |

## Event flow

Windows Security, System, Application, and Sysmon events are collected by the Wazuh agent, sent to the manager, and made searchable in the dashboard. I also configured FIM for `C:\\SOC-Lab` to test file creation and modification alerts.

The VM uses VirtualBox networking with local port forwarding for dashboard access. This setup is only intended for local practice; I have not built a multi-host or production environment.
