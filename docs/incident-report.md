# Sample SOC Triage Notes

## Case A — Windows failed logon
**Category:** Authentication  
**Evidence:** Windows Event ID 4625; Wazuh rule 60122, level 5  
**Observed context:** Interactive logon type, loopback source address, process path under `C:\\Windows\\System32\\svchost.exe`, Negotiate authentication package.

### Initial assessment
A failed logon was recorded. The event alone does not establish whether the cause was a mistyped credential, a local application/service, routine system behavior, or malicious activity.

### Triage checklist
- [ ] Confirm timestamp and host context.
- [ ] Inspect target username and logon process.
- [ ] Correlate with nearby 4624 successful-logon events and other 4625 failures.
- [ ] Check process creation and service activity around the same time.
- [ ] Confirm whether the account and activity are expected.
- [ ] Document disposition and supporting evidence.

**Disposition:** Inconclusive from the available single-event context. Additional correlation is required.

## Case B — File integrity alert
**Category:** File integrity monitoring  
**Evidence:** Wazuh rule 550 for a modified file and rule 554 for a newly created file in `C:\\SOC-Lab`.

### Initial assessment
The changes were intentionally made as lab validation tests. The expected FIM alerts were generated, confirming the configured monitor detects file changes in the test directory.

### Triage checklist
- [x] Confirm alert references the monitored directory.
- [x] Check whether the change aligns with the planned test.
- [ ] In a real investigation, identify the process/user responsible for the change.
- [ ] Compare file hashes and assess file contents in a safe environment if unexpected.

**Disposition:** Expected lab activity; detection validated.

## Analyst note
Severity and ATT&CK mappings are triage aids, not verdicts. A reliable conclusion requires context, corroboration, and documentation of uncertainty.
