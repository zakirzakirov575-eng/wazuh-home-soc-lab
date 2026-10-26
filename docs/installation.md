# Setup Notes

These are the main setup details from my lab.

## Environment

- Windows 11 host
- Ubuntu virtual machine in Oracle VirtualBox
- Wazuh 4.14.9
- Windows Wazuh agent
- Sysmon

The installer warned that my Ubuntu release was not on its recommended OS list. The dashboard eventually loaded at `https://127.0.0.1:8443`. The browser showed a certificate warning because the lab uses a local certificate.

## Windows agent

The agent appeared in the dashboard as `Windows-Host`, ID `001`, with status **Active**.

The agent configuration file is:

`C:\\Program Files (x86)\\ossec-agent\\ossec.conf`

I enabled collection for Windows Application, Security, System, and `Microsoft-Windows-Sysmon/Operational` events.

## File integrity monitoring

I configured `C:\\SOC-Lab` for real-time monitoring. I then modified an existing test file and created another one. Wazuh generated alerts for both changes.

## Things I ran into

- The dashboard certificate was not trusted by the browser.
- At one point the dashboard reported an API selection error.
- The installer showed an OS compatibility warning.

This was a learning setup, so I checked the dashboard and agent status as I went. The lab dashboard should stay local and should not be exposed directly to the internet.
