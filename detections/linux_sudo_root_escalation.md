## SPL Query
index=task5
| search "sudo" "root"
| table _time host user _raw
| sort - _time


## Purpose
Used to identify which user escalated privileges to root prior to the creation of the remote-ssh account. This confirms the privilege escalation step in the attacker’s progression.










KQL (Microsoft Sentinel – Equivalent Detection Logic)
LinuxLogs
| where Message has "sudo" and Message has "root"
| project TimeGenerated, host, user, Message
| order by TimeGenerated desc


What Changed (SPL → KQL)

index=task5 becomes selecting a table in KQL (example: LinuxLogs).

search "sudo" "root" becomes a where condition using Message has.

table in SPL becomes project in KQL.

_time becomes TimeGenerated.

sort - _time becomes order by TimeGenerated desc.
