# Web URI Volume Analysis

## SPL Query
```spl
index=task6
| stats count by uri_path
| sort -count


Purpose

This query aggregates web requests by URI path to identify which endpoint received the highest traffic volume. Sorting by count revealed abnormal request volume directed at /wp-login.php, indicating a likely authentication-focused attack.




KQL (Microsoft Sentinel – Equivalent Detection Logic)
WebLogs
| summarize request_count = count() by uri_path
| order by request_count desc
What Changed (SPL → KQL)

index=task6 becomes selecting a table in KQL (example: WebLogs).

stats count by uri_path becomes summarize count() by uri_path.

sort -count in SPL becomes order by request_count desc in KQL.
