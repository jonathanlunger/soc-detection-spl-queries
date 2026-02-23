# Brute Force – WordPress Login Failures

## SPL Query
```spl
index=task6 src_ip=10.10.243.134 "/wp-login.php" "POST"
| search ("401" OR "403" OR "failed")
| stats count as failed_attempts

Explanation

This query searches the task6 index for POST requests to /wp-login.php coming from the source IP 10.10.243.134. It filters for common login failure indicators such as HTTP status codes 401, 403, or the keyword failed. The stats count command totals the number of failed login attempts from that source, which may indicate brute force behavior if the count is high.

SOC Relevance

Multiple failed POST login attempts may indicate brute force or password spraying activity.

The source IP should be investigated for additional reconnaissance or malicious behavior.

If confirmed malicious, block the IP and review authentication logs for successful logins after failures.

Tuning

Increase threshold using | where failed_attempts > 5 to reduce false positives.

Exclude known internal scanners or vulnerability assessment tools.

Add time window constraints using bin _time span=5m.
