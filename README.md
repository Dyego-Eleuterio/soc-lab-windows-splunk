# SOC Lab #1 – Sysmon + Splunk (Log Collection & Analysis)

## 📌 Overview
This project is a hands-on Cybersecurity lab focused on log collection and analysis using Sysmon and Splunk. The goal is to simulate a basic Security Operations Center (SOC) environment, where system activity is monitored, collected, and analyzed to identify potential security events.

---

## 🛠️ Tools & Technologies
- Sysmon (System Monitor)
- Splunk Enterprise (SIEM)
- Splunk Universal Forwarder
- Windows 10 Virtual Machine
- Windows Event Logs

---

## 🧱 Lab Architecture
Sysmon → Windows Event Logs → Splunk Universal Forwarder → Splunk Enterprise

---

## ⚙️ Configuration Steps

### 1. Sysmon Installation
- Download Sysmon from Microsoft Sysinternals  
- Install:

    sysmon64.exe -i

- Verify:
Event Viewer → Microsoft → Windows → Sysmon → Operational  

---

### 2. Splunk Setup
Access:
    
    http://localhost:8000

---

### 3. Forwarder Configuration

    splunk add forward-server 127.0.0.1:9997

---

### 4. Enable Sysmon Logs

Edit:

    C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf

Add:

    [WinEventLog://Microsoft-Windows-Sysmon/Operational]
    disabled = 0
    index = main

Restart:

    splunk restart

---

## 🔍 Log Analysis (Splunk Queries)

Below are examples of searches performed during the lab:

### 📌 Process Creation (Sysmon Event ID 1)

    index=* EventCode=1

Used to monitor process execution on the system.

---

### 📌 Failed Logon Attempts (Security Event ID 4625)

    index=* EventCode=4625

Used to identify failed login attempts.

---

### 📌 Successful Logons (Event ID 4624)

    index=* EventCode=4624

Useful to track user authentication activity.

---

### 📌 PowerShell Activity

    index=* powershell

Helps identify PowerShell usage, which is often leveraged in attacks.

---

### 📌 All Windows Logs Overview

    index=*

General exploration of all ingested logs.

---

## ⚠️ Challenges Faced

Configuring Sysmon to properly send logs to Splunk was the biggest challenge.

It took approximately **3 days of troubleshooting**, involving:

- Fixing incorrect file extension (`inputs.conf.txt`)
- Adjusting forwarder configuration
- Validating log ingestion pipeline

---

## 🎯 Key Learnings
- Log ingestion and forwarding
- SIEM fundamentals
- Event correlation basics
- Troubleshooting data pipelines
- Visibility into endpoint activity

---

## 🚀 Next Steps
- Create detection rules (use cases)
- Simulate attacks (Brute force, PowerShell abuse)
- Build dashboards in Splunk
- Start basic threat hunting

---

## 📸 Screenshots
- Splunk results for EventCode=1
- Failed login attempts (4625)
- Sysmon logs in Event Viewer

---

## 👨‍💻 Author
Dyego Eleutério  
IT Support Analyst transitioning into Cybersecurity

