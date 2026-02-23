## SPL Query
index=task5
| search ("cron" OR "crontab" OR "/etc/cron" OR "CRON")
| table _time host user port _raw
| sort - _time

## Purpose
Used to identify the persistence mechanism established on the system. Searching cron activity and displaying the port field reveals the configured port used in the persistence job (recurring access via cron).





KQL (Microsoft Sentinel – Equivalent Detection Logic)
LinuxLogs
| where Message has "cron" 
    or Message has "crontab" 
    or Message has "/etc/cron"
| project TimeGenerated, host, user, port, Message
| order by TimeGenerated desc
What Changed (SPL → KQL)

index=task5 becomes selecting a table in KQL (example: LinuxLogs).

search (...) becomes multiple where conditions using Message has.

table becomes project to select fields.

_time becomes TimeGenerated.

sort - _time becomes order by TimeGenerated desc.
