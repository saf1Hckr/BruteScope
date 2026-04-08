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

![Kali Linux](https://github.com/saf1Hckr/BruteScope/blob/main/Hydra_Brute_Force.png)

- Manual SSH login attempts for simulation

![SSH](https://github.com/saf1Hckr/BruteScope/blob/main/SSH_Manual.png)

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
index=soc_logs "Failed password"
| stats count by src_ip
| where count > 10
```

![Failed Count](https://github.com/saf1Hckr/BruteScope/blob/main/SSH_Count_Failed.png)

2️⃣ All Failed attempts:

I created an extra Field "action" only to record all the failed attempts with brute force attack
```splunk
index=soc_logs | stats count by action | where count > 10
```

![Bar Chart](https://github.com/saf1Hckr/BruteScope/blob/main/Bar_Chart.png)

![Pie Chart](https://github.com/saf1Hckr/BruteScope/blob/main/Pie_chart.png)

## 📊 Splunk Visualization 
- Column Chart: Number of failed login attempts per IP 
- Timechart: Failed attempts over time 

## 🧠 Learning Outcomes 
- Understand SSH brute force attack patterns 
- Learn Linux authentication logging (`/var/log/auth.log`) 
- Use Splunk for threat detection and visualization 
- Apply MITRE ATT&CK techniques: T1110 – Brute Force 

## 🔎 Findings and Observation

- SSH brute force activity generated multiple failed login attempts in `/var/log/auth.log`
- Attack traffic from the Kali Linux machine was successfully recorded on the Ubuntu target
- A dedicated Splunk index (`soc_logs`) was created to separate security events from the default `main` index
- A Splunk Universal Forwarder was configured on the Kali Linux machine to simulate log forwarding from an attacker environment
- Ingestion was configured using port **9997** on the Splunk instance (EC2), enabling secure log forwarding
- Authentication logs from the Ubuntu server were monitored and ingested into Splunk for analysis
- Multiple failed login attempts from a single IP clearly indicated brute force attack behavior
- Repeated login attempts using different usernames suggested username enumeration activity

