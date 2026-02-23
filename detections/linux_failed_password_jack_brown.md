## SPL Query
index=task5
| search "Failed password" jack-brown
| table _time _raw
| sort 0 _time

## Purpose
Used to count failed authentication attempts for the user jack-brown prior to a successful login. Repeated failures indicate brute force behavior before access was achieved.
