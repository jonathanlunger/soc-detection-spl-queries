## SPL Query
index=task5
| search ("cron" OR "crontab" OR "/etc/cron" OR "CRON")
| table _time host user port _raw
| sort - _time

## Purpose
Used to identify the persistence mechanism established on the system. Searching cron activity and displaying the port field reveals the configured port used in the persistence job (recurring access via cron).
