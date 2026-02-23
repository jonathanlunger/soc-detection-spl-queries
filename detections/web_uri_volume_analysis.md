# Web URI Volume Analysis

## SPL Query
```spl
index=task6
| stats count by uri_path
| sort -count


Purpose

This query aggregates web requests by URI path to identify which endpoint received the highest traffic volume. Sorting by count revealed abnormal request volume directed at /wp-login.php, indicating a likely authentication-focused attack.
