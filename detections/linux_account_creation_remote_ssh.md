## SPL Query
index=task5
| search ("useradd" OR "new user" OR "remote-ssh")
| sort 0 _time
| table _time host user _raw

## Purpose
Used to identify the timestamp associated with the creation of the remote-ssh account. This helps confirm when persistence was established through the creation of a new user account.
