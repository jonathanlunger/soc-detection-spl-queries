# Brute Force –  Login Failures

## SPL Query
```spl
index=task6 src_ip=10.10.243.134 "/wp-login.php" "POST"
| search ("401" OR "403" OR "failed")
| stats count as failed_attempts

Purpose

Detects repeated failed login attempts against WordPress. Multiple POST requests to /wp-login.php returning authentication failures may indicate brute force or password spraying activity from a single source IP.



## KQL (Microsoft Sentinel – Equivalent Detection Logic)

WebLogs
| where src_ip == "10.10.243.134"
| where uri_path == "/wp-login.php"
| where method == "POST"
| where status in ("401","403") or Message has "failed"
| summarize failed_attempts = count()

What Changed (SPL → KQL)

index=task6 becomes choosing a table in KQL (example: WebLogs).

SPL filters become where statements in KQL.

search in SPL becomes another where condition in KQL.

stats count in SPL becomes summarize count() in KQL.

Raw text searching uses Message has in KQL.
