## SPL Query
index=task5
| search "Failed password" jack-brown
| table _time _raw
| sort 0 _time

## Purpose
Used to count failed authentication attempts for the user jack-brown prior to a successful login. Repeated failures indicate brute force behavior before access was achieved.



## KQL (Microsoft Sentinel – Equivalent Detection Logic)

```kql
LinuxLogs
| where Message has "Failed password" and Message has "jack-brown"
| project TimeGenerated, Message
| order by TimeGenerated asc
What Changed (SPL → KQL)

index=task5 becomes selecting a table in KQL (example: LinuxLogs).

search becomes a where condition using Message has.

table becomes project to choose specific columns.

_time becomes TimeGenerated.

sort 0 _time becomes order by TimeGenerated asc.
