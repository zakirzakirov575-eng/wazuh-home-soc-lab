# Wazuh Searches

These are the Discover filters I used or kept for checking events in this lab. Field names can vary by Wazuh version and index pattern, so I check the event JSON if a filter does not match.

## Failed Windows logons (Event ID 4625)

```text
agent.name: "Windows-Host" AND data.win.system.eventID: 4625
```

This is useful for finding failed logons on the Windows endpoint. I check the account, logon type, source, status, and events around the same time.

## Sysmon process creation (Event ID 1)

```text
data.win.system.channel: "Microsoft-Windows-Sysmon/Operational" AND data.win.system.eventID: 1
```

This searches Sysmon process-creation events. Useful fields include the image, command line, parent process, user, hashes, and timestamp.

## File integrity alerts

I look for Wazuh rule **550** for a modified file and **554** for a newly created file. Both tests were done in `C:\\SOC-Lab`.

For any of these searches, the event needs context before I can decide whether it is suspicious.
