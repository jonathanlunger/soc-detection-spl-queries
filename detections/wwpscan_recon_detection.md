# WPScan Detection – WordPress Reconnaissance

## SPL Query
```spl
index=task6 src_ip=10.10.243.134
| search "WPScan"
| stats count as scan_events by src_ip

Purpose

Detects the use of the WPScan tool against a WordPress application. WPScan is commonly used for enumeration and vulnerability discovery. Identifying this activity helps detect reconnaissance behavior that may precede brute force or exploitation attempts.
