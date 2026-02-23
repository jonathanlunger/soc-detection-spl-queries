## SPL Query
index=task5
| search "sudo" "root"
| table _time host user _raw
| sort - _time


## Purpose
Used to identify which user escalated privileges to root prior to the creation of the remote-ssh account. This confirms the privilege escalation step in the attacker’s progression.
