# Brute Force – WordPress Login Failures

## SPL Query
```spl
index=task6 src_ip=10.10.243.134 "/wp-login.php" "POST"
| search ("401" OR "403" OR "failed")
| stats count as failed_attempts

Purpose

Detects repeated failed login attempts against WordPress. Multiple POST requests to /wp-login.php returning authentication failures may indicate brute force or password spraying activity from a single source IP.
