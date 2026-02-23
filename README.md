# soc-detection-spl-queries

---

# **Investigation Context and Log Sources**

## **Overview**

The detections in this repository were developed during a structured security investigation involving Windows event logs, Linux system logs, and web application logs. The objective was to identify attacker behavior across multiple systems, confirm persistence mechanisms, and reconstruct the attack timeline using log analysis.

Each detection reflects investigative reasoning rather than simple keyword searching. Queries were built to answer specific forensic questions and validate attacker progression.

---

## **Windows Log Analysis (Authentication & Privilege Escalation)**

The Windows portion of the investigation focused on identifying:

- Failed and successful authentication attempts  
- Potential brute force activity  
- Privilege escalation behavior  
- Account creation or suspicious administrative actions  

The goal was to determine whether an attacker gained access through repeated authentication attempts and whether elevated privileges were obtained after initial compromise.

Windows event logs are highly structured, so the analysis emphasized:
- Authentication event patterns
- User activity correlation
- Escalation from standard user to administrative privileges
- Timeline reconstruction using event timestamps

---

## **Linux Log Analysis (Persistence & Root Activity)**

The Linux investigation centered on system-level attacker activity, specifically:

- Failed SSH login attempts (brute force behavior)
- Successful authentication following repeated failures
- Use of `sudo` to escalate privileges to root
- Creation of new user accounts (e.g., remote-ssh)
- Cron-based persistence mechanisms

The objective was to confirm:

1. Initial access method  
2. Privilege escalation to root  
3. Persistence via scheduled cron jobs  
4. Long-term access mechanisms  

Linux logs required searching raw message fields and correlating events chronologically to identify attacker progression.

---

## **Web Application Log Analysis (WordPress Attack Activity)**

The web application logs focused on a WordPress environment and were used to detect:

- Abnormal traffic volume to `/wp-login.php`
- Repeated failed POST login attempts
- Authentication failure status codes (401 / 403)
- Identification of automated tooling (WPScan) via user-agent inspection

The investigation revealed:

- Authentication-focused brute force activity
- Automated reconnaissance prior to exploitation
- High-volume login attempts from a single source IP
- Use of WPScan as the attack tool

This portion demonstrated how web logs can expose both reconnaissance and exploitation phases of an attack.

---

# **Detection Logic Methodology**

## **Breaking Down the Logic (SPL Development)**

Each SPL query was constructed by:

1. Identifying the investigative question  
2. Narrowing logs using relevant fields or raw text search  
3. Aggregating or sorting events to reveal patterns  
4. Confirming attacker behavior through timeline analysis  

Rather than writing broad searches, each query was designed to validate a specific hypothesis (e.g., brute force, privilege escalation, persistence).

---

## **Cross-Platform Translation (SPL → KQL)**

To demonstrate understanding beyond a single SIEM platform, each detection was translated from Splunk Processing Language (SPL) to Kusto Query Language (KQL) for Microsoft Sentinel.

The conversion required:

- Mapping `index=` to selecting a table
- Converting `search` statements into structured `where` clauses
- Translating `stats` into `summarize`
- Converting `table` into `project`
- Replacing `_time` with `TimeGenerated`
- Adapting raw text searches using `Message has`

This process demonstrates comprehension of detection logic independent of tooling. The goal was not to memorize syntax, but to understand how investigative reasoning transfers between SIEM environments.

---

## **Key Takeaway**

This repository represents:

- Multi-platform log analysis (Windows, Linux, Web)
- Structured investigative methodology
- Detection engineering thinking
- Cross-SIEM query translation capability

The emphasis is on logic, pattern recognition, and attacker behavior reconstruction — not just query execution.
