# Recon Scanning – Excessive Web Requests from Single Source

## SPL Query
```spl
index=task6 src_ip=10.10.243.134
| stats count as request_count values(uri_path) as accessed_paths by src_ip
| where request_count > 50
| sort - request_count

Purpose

Detects high-volume web requests from a single source IP. A large number of requests to different URI paths may indicate automated reconnaissance or directory enumeration activity prior to exploitation attempts.
