# WordPress Brute Force Detection

## SPL Query
```spl
index=task6 src_ip=10.10.243.134 "/wp-login.php" "POST"
| search ("401" OR "403" OR "failed")
| stats count

Purpose

This query counts failed login attempts originating from the source IP address 10.10.243.134. Filtering specifically for POST requests to /wp-login.php and failed status indicators confirms repeated authentication failures consistent with brute force behavior.





KQL (Microsoft Sentinel – Equivalent Detection Logic)
WebLogs
| where src_ip == "10.10.243.134"
| where uri_path == "/wp-login.php"
| where method == "POST"
| where status in ("401","403") or Message has "failed"
| summarize failed_attempts = count()
What Changed (SPL → KQL)

index=task6 becomes selecting a table in KQL (example: WebLogs).

Inline filters in SPL become where statements in KQL.

search becomes another where condition.

stats count becomes summarize count().

Raw text matching uses Message has in KQL.
