## SPL Query
index=task5
| search ("useradd" OR "new user" OR "remote-ssh")
| sort 0 _time
| table _time host user _raw

## Purpose
Used to identify the timestamp associated with the creation of the remote-ssh account. This helps confirm when persistence was established through the creation of a new user account.




## KQL (Microsoft Sentinel – Equivalent Detection Logic)

```kql
LinuxLogs
| where Message has "useradd"
    or Message has "new user"
    or Message has "remote-ssh"
| order by TimeGenerated asc
| project TimeGenerated, host, user, Message
What Changed (SPL → KQL)

index=task5 becomes selecting a table in KQL (example: LinuxLogs).

search (...) becomes where conditions using Message has.

sort 0 _time becomes order by TimeGenerated asc.

table becomes project to select specific columns.

_time becomes TimeGenerated.
