---
layout: default
title: Security Monitoring Lab (Wazuh + Cowrie)
---

<div style="text-align: right;">
  <a href="https://github.com/Jiubel/security-monitoring-lab" target="_blank" class="github-btn">
    View on GitHub →
  </a>
</div>

# 🛡️ Security Monitoring Lab (Wazuh + Cowrie Honeypot)

## Overview
Designed and implemented a security monitoring lab to simulate attacker behavior and analyze how events are captured, processed, and detected within a SIEM.

The environment consists of a Cowrie SSH honeypot generating attacker activity and a Wazuh SIEM ingesting, analyzing, and generating alerts based on that activity through custom detection rules.

---

## Lab Architecture

![Lab Diagram](/screenshots/soc-lab-architecture.png)

---

## Key Components

### Cowrie Honeypot (Ubuntu VM)
- SSH Honeypot (Port 2222)
- Captures attacker commands and session activity
- Logs stored in JSON format (cowrie.json)
- Simulates a vulnerable Linux system

### Wazuh SIEM (Ubuntu VM)
- Centralized log ingestion and analysis
- Wazuh Agent for log forwarding
- Event parsing and rule-based detection
- Alert generation via Wazuh dashboard

### Detection Pipeline
- Attacker connects via SSH to honeypot
- Cowrie logs activity in JSON format
- Wazuh agent forwards logs to SIEM
- Custom detection rules identify command execution
- Alerts generated and visualized in dashboard

---

## Detection Engineering

Created a custom Wazuh rule to detect command execution within the honeypot environment:

<rule id="100201" level="5">
  <decoded_as>json</decoded_as>
  <field name="eventid">^cowrie\.command\.input$</field>
  <description>Cowrie command executed: $(input)</description>
</rule>

---

## Validation

### Attack Simulation
Simulated attacker activity by connecting to the honeypot via SSH and executing commands:

ssh -p 2222 root@localhost  
whoami  
exit  

![SSH Simulation](/screenshots/04-ssh-attack-simulation.png)

---

### Log Ingestion Verification
Confirmed that Cowrie logs were successfully ingested and parsed by Wazuh.

![Wazuh Events](/screenshots/08-wazuh-events-ingested.png)

---

### Alert Generation
Validated that custom detection rules triggered alerts based on attacker commands.

![Detection Alert](/screenshots/11-detection-alert-triggered.png)

---

## Key Skills Demonstrated

- SIEM Monitoring (Wazuh)  
- Log Ingestion & Analysis  
- Detection Rule Development  
- Security Event Investigation  
- Linux System Administration  
- Honeypot Deployment  
- Troubleshooting & Debugging  

---

## Summary
This project simulates a real-world security monitoring pipeline by integrating a honeypot with a SIEM to capture, analyze, and detect attacker behavior.

It demonstrates practical experience in log ingestion, detection engineering, and alert validation, reflecting core workflows performed by SOC analysts in identifying and responding to security events.
