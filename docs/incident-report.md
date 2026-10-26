# Triage Notes

These notes cover two things I checked in the lab.

## Failed Windows logon

**Event:** Windows Event ID 4625  
**Wazuh rule:** 60122, level 5

The event I inspected showed an interactive logon type, source address `127.0.0.1`, process `C:\\Windows\\System32\\svchost.exe`, and authentication package `Negotiate`.

I could confirm that a logon failed, but not why it failed. A single event is not enough to call this an attack. To understand it better, I would need to check the target account, timestamp, nearby 4625 and 4624 events, and related process or service activity.

**Assessment:** Inconclusive with the information I collected.

## File integrity monitoring

I deliberately changed `C:\\SOC-Lab\\test.txt` and created `C:\\SOC-Lab\\soc-test-2.txt`.

- Rule 550 appeared for the modified file.
- Rule 554 appeared for the new file.

These were expected results from my own tests, so I treated them as successful FIM checks rather than incidents.

## Takeaway

An alert tells me what matched a rule. I still need surrounding event data to decide whether the activity is expected or suspicious.
