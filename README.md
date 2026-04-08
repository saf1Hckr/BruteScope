# BruteScope

**SSH Brute Force Detection & Analysis using Splunk**

## 🚀 Project Overview

BruteScope is a cybersecurity SOC lab project designed to detect and analyze SSH brute force attacks.
The setup simulates attacks using a Kali Linux attacker against an Ubuntu target. Logs are collected and visualized in Splunk to identify suspicious login attempts and patterns.
This project demonstrates real-world detection methods for SOC analysts and highlights the importance of monitoring authentication events in Linux systems.

## 🖥️ Lab Setup

| Component | Role |
| --- | --- |
| Kali Linux | Attacker machine, performs brute force using Hydra |
| Ubuntu Server | Target machine, SSH service enabled |
| Splunk | SIEM for log ingestion, analysis, and visualization |

### Attack Tools:
- Hydra (`hydra -l <username> -P <password-list> ssh://<target-ip>`)
- Manual SSH login attempts for simulation

### Target Logs:
- `/var/log/auth.log` (Ubuntu SSH authentication logs)

## 🔍 Detection Methodology

BruteScope detects brute force attacks by analyzing:
- Multiple failed login attempts from the same IP
- Multiple usernames attempted from the same IP
- Sudden successful login after multiple failures

## Example Splunk Queries
1️⃣ Count failed SSH attempts by IP:
```splunk
index=linux_logs "Failed password"
| stats count by src_ip
| where count > 10
```
2️⃣ Failed vs successful attempts:
```splunk
index=linux_logs ("Failed password" OR "Accepted password")
| stats count(eval(searchmatch("Failed password"))) as failed_attempts,
        count(eval(searchmatch("Accepted password"))) as success_attempts
        by src_ip
| where failed_attempts > 10
```

## 📊 Splunk Visualization 
- Bar Chart: Number of failed login attempts per IP 
- Timechart: Failed attempts over time 
- Alerts: Trigger alert if failed attempts exceed threshold 

## 🧠 Learning Outcomes 
- Understand SSH brute force attack patterns 
- Learn Linux authentication logging (`/var/log/auth.log`) 
- Use Splunk for threat detection and visualization 
- Apply MITRE ATT&CK techniques: T1110 – Brute Force 

## ⚡ Usage 
1. Clone the repository:
git clone [https://github.com/](https://github.com/)<your-username>/BruteScope.git
dd BruteScope/
db cd BruteScope/
db  
b2. Set up your Ubuntu server and enable SSH logs.
b3. Configure Splunk to ingest `/var/log/auth.log`.
b4. Simulate brute force attacks using Kali Linux + Hydra.
b5. Run the Splunk queries provided to detect attack patterns.

## 📁 Repository Structure 
```
brutescope/
total-	README.md
total-	splunk_queries/
total-	failed_attempts_search.spl
total-	failed_vs_success_search.spl
total-	screenshots/
total-	failed_attempts_chart.png
total-	timechart.png
total-	notes/
total-	lab_observations.txt```
'throughout' 'the structure.'
default 'Markdown' format.# BruteScope

**SSH Brute Force Detection & Analysis using Splunk**

## 🚀 Project Overview

BruteScope is a cybersecurity SOC lab project designed to detect and analyze SSH brute force attacks.
The setup simulates attacks using a Kali Linux attacker against an Ubuntu target. Logs are collected and visualized in Splunk to identify suspicious login attempts and patterns.
This project demonstrates real-world detection methods for SOC analysts and highlights the importance of monitoring authentication events in Linux systems.

## 🖥️ Lab Setup

| Component | Role |
| --- | --- |
| Kali Linux | Attacker machine, performs brute force using Hydra |
| Ubuntu Server | Target machine, SSH service enabled |
| Splunk | SIEM for log ingestion, analysis, and visualization |

### Attack Tools:
- Hydra (`hydra -l <username> -P <password-list> ssh://<target-ip>`)
- Manual SSH login attempts for simulation

### Target Logs:
- `/var/log/auth.log` (Ubuntu SSH authentication logs)

## 🔍 Detection Methodology

BruteScope detects brute force attacks by analyzing:
- Multiple failed login attempts from the same IP
- Multiple usernames attempted from the same IP
- Sudden successful login after multiple failures

## Example Splunk Queries
1️⃣ Count failed SSH attempts by IP:
```splunk
index=linux_logs "Failed password"
| stats count by src_ip
| where count > 10
```
2️⃣ Failed vs successful attempts:
```splunk
index=linux_logs ("Failed password" OR "Accepted password")
| stats count(eval(searchmatch("Failed password"))) as failed_attempts,
        count(eval(searchmatch("Accepted password"))) as success_attempts
        by src_ip
| where failed_attempts > 10
```

## 📊 Splunk Visualization 
- Bar Chart: Number of failed login attempts per IP 
- Timechart: Failed attempts over time 
- Alerts: Trigger alert if failed attempts exceed threshold 

## 🧠 Learning Outcomes 
- Understand SSH brute force attack patterns 
- Learn Linux authentication logging (`/var/log/auth.log`) 
- Use Splunk for threat detection and visualization 
- Apply MITRE ATT&CK techniques: T1110 – Brute Force 

## ⚡ Usage 
1. Clone the repository:
git clone [https://github.com/](https://github.com/)<your-username>/BruteScope.git
dd BruteScope/
db cd BruteScope/
db  
b2. Set up your Ubuntu server and enable SSH logs.
b3. Configure Splunk to ingest `/var/log/auth.log`.
b4. Simulate brute force attacks using Kali Linux + Hydra.
b5. Run the Splunk queries provided to detect attack patterns.

## 📁 Repository Structure 
```
brutescope/
total-	README.md
total-	splunk_queries/
total-	failed_attempts_search.spl
total-	failed_vs_success_search.spl
total-	screenshots/
total-	failed_attempts_chart.png
total-	timechart.png
total-	notes/
total-	lab_observations.txt```
'throughout' 'the structure.'
default 'Markdown' format.
