# Wazuh Hunting Queries

These examples are dashboard Discover filters for the lab. Field availability depends on Wazuh version, index pattern, and event decoder. If a field does not resolve, inspect an event's JSON and adapt the field name.

## Windows failed logons — Event ID 4625

```text
agent.name: "Windows-Host" AND data.win.system.eventID: 4625
```

Purpose: Find failed Windows logons for the monitored endpoint. Review target account, logon type, source address, process, status/substatus, and neighboring events.

## Sysmon process creation — Event ID 1

```text
data.win.system.channel: "Microsoft-Windows-Sysmon/Operational" AND data.win.system.eventID: 1
```

Purpose: Search Sysmon process creation events. Investigate process image, command line, parent process, user, hashes, and timestamp. Do not assume a process is malicious solely because a rule fired.

## FIM events
Start with the monitored agent and look for FIM rule IDs **550** (integrity checksum changed) and **554** (file added). Field names can vary by index pattern; use the alert's rule ID and inspect the event JSON.

## Practical triage sequence
1. Set an appropriate time range.
2. Filter by endpoint and event/rule ID.
3. Open the full event and capture relevant fields.
4. Search for related events within a few minutes before and after.
5. Decide whether the event is expected, suspicious, or inconclusive.
6. Record evidence and confidence; avoid declaring an incident without corroboration.
