# WordPress Brute Force Detection

## SPL Query
```spl
index=task6 src_ip=10.10.243.134 "/wp-login.php" "POST"
| search ("401" OR "403" OR "failed")
| stats count

Purpose

This query counts failed login attempts originating from the source IP address 10.10.243.134. Filtering specifically for POST requests to /wp-login.php and failed status indicators confirms repeated authentication failures consistent with brute force behavior.
