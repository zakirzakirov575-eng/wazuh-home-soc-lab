# Detection Results

These are the results I observed while testing my Wazuh lab.

## 1. File modification

I changed `C:\\SOC-Lab\\test.txt`.

- Rule: **550**
- Level: **7**
- Description: Integrity checksum changed
- Decoder: `syscheck_integrity_changed`
- File size: 31 bytes → 52 bytes

SHA-256 before:
`b5e29c8d4e6c8f3dfaf035bf16308623d8b95b9dd540df77d14e02989598bd5e`

SHA-256 after:
`9488476ae7a95964419cdd5a3dafc5eb089ebbeaeb045cbd6f54e483a0d9c328`

The hash and size changed, and Wazuh detected the modification.

## 2. New file

I created `C:\\SOC-Lab\\soc-test-2.txt`.

- Rule: **554**
- Level: **5**
- Description: File added to the system
- SHA-256: `07e780d2104c77b3d7d0c642e6da32dba2800fe3a0879559f13077204e36752a`

Wazuh detected the new file in the monitored directory.

## 3. Failed logons

I searched for Windows Event ID **4625** and found two matching events in the selected 24-hour period.

- Wazuh rule: **60122**
- Level: **5**
- Logon type: **2** (interactive)
- Source: `127.0.0.1`
- Process: `C:\\Windows\\System32\\svchost.exe`
- Authentication package: `Negotiate`
- Status: `0xc000006d`

This confirms that failed-logon events were collected and searchable. I do not have enough context to say why these logons failed or whether they were suspicious.

## 4. Sysmon

Events from `Microsoft-Windows-Sysmon/Operational` appeared in Wazuh. I also saw an alert for `sdbinst.exe` under rule **92058**, level **12**, associated with ATT&CK technique **T1546.011**.

The alert is worth investigating, but the event alone does not prove malicious activity.

## 5. Vulnerability detection

The dashboard showed a vulnerability finding for Oracle VirtualBox 7.2.16, including **CVE-2026-87285** with Medium severity and CVSS 3.1 score 6.0.

A version match in vulnerability detection is not evidence that the vulnerability was exploited. The installed version and vendor advisory would need to be checked before deciding what to do about the finding.

## Summary

So far, I have verified FIM alerts for file creation and modification, searchable failed-logon events, Sysmon event collection, and vulnerability findings in the Wazuh dashboard.
