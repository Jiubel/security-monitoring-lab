# 🛡️ Security Monitoring Lab (Wazuh + Cowrie Honeypot)

## Summary
This project showcases a practical implementation of a security monitoring pipeline using a SIEM (Wazuh) and a honeypot (Cowrie) to simulate attacker activity and build custom detections from real log data.

The environment replicates a simplified SOC workflow, where attacker behavior is captured, processed, analyzed, and converted into actionable alerts.

---

## 📌 Objective
The objective of this lab was to design and implement an end-to-end detection pipeline that demonstrates how security events are generated, ingested, and analyzed within a SIEM.

Rather than focusing solely on tool deployment, this project emphasizes:
- Log generation through simulated attacks  
- Centralized log ingestion  
- Detection engineering using custom rules  
- Validation of alerts based on real activity  

---

## 🧱 Technologies Used
- Wazuh (SIEM / log analysis)
- Cowrie (SSH honeypot)
- Oracle VirtualBox (lab environment)
- Ubuntu Linux

---

## 🏗️ Architecture

The lab is structured as a security monitoring pipeline:

- An attacker interacts with a simulated SSH service (Cowrie)
- Cowrie logs all activity in JSON format
- The Wazuh agent forwards logs to the Wazuh manager
- The SIEM processes events and applies detection rules
- Alerts are generated and visualized in the dashboard

![SOC Lab Architecture](screenshots/soc-lab-architecture.png)

---

## ⚙️ Implementation Overview

### Wazuh Deployment
Wazuh was deployed and configured as the central SIEM platform for log ingestion, processing, and alerting. The dashboard was validated to ensure visibility into incoming events.

![Wazuh Dashboard](screenshots/02-wazuh-dashboard-overview.png)

---

### Cowrie Honeypot Deployment
Cowrie was configured as an SSH honeypot listening on port 2222, emulating a vulnerable system to capture attacker interactions.

![Cowrie Running](screenshots/03-cowrie-honeypot-running.png)

---

### Attack Simulation
Simulated attacker activity was performed by connecting to the honeypot via SSH and executing commands such as:

    ssh -p 2222 root@localhost
    whoami
    exit

![SSH Attack Simulation](screenshots/04-ssh-attack-simulation.png)

---

### Log Collection & Verification
Cowrie logs were verified at the source to confirm that attacker commands and session data were being recorded in JSON format.

![Cowrie Logs](screenshots/05-cowrie-raw-logs.png)

---

### Log Ingestion (Wazuh Agent)
The Wazuh agent was deployed on the Cowrie host and configured to forward logs to the SIEM.

A localfile configuration was added to ingest Cowrie logs:

    <localfile>
      <log_format>json</log_format>
      <location>/home/cowrie/cowrie/var/log/cowrie/cowrie.json</location>
    </localfile>

![Log Ingestion Config](screenshots/07-wazuh-log-ingestion-config.png)

---

### Event Visibility in SIEM
Once ingestion was configured, logs were successfully visualized in the Wazuh dashboard, confirming end-to-end data flow.

![Wazuh Events](screenshots/08-wazuh-events-ingested.png)

---

### Detection Engineering
A custom detection rule was created to identify command execution within the honeypot environment:

    <rule id="100201" level="5">
      <decoded_as>json</decoded_as>
      <field name="eventid">^cowrie\.command\.input$</field>
      <description>Cowrie command executed: $(input)</description>
    </rule>

![Custom Rule](screenshots/09-custom-detection-rule.png)

---

### Rule Validation
The detection rule was tested using the Wazuh logtest utility to confirm proper parsing and alert generation.

![Rule Testing](screenshots/10-rule-testing-wazuh-logtest.png)

---

### Alert Generation & Verification
Additional attacker activity was simulated, and alerts were successfully generated and observed in the Wazuh dashboard.

![Alert Triggered](screenshots/11-detection-alert-triggered.png)

---

## 📊 Results
- Simulated SSH-based attacker behavior  
- Captured and structured logs using a honeypot  
- Forwarded logs into a centralized SIEM  
- Developed and validated a custom detection rule  
- Generated alerts based on real command execution  

---

## 📚 Key Takeaways
- Understanding of SIEM ingestion pipelines and event processing  
- Practical experience with honeypot-based threat simulation  
- Ability to create and validate detection rules  
- Hands-on experience with log analysis and event correlation  
- Insight into how attacker behavior translates into SIEM alerts  

---

## 🚀 Skills Demonstrated
- SIEM Monitoring (Wazuh)  
- Log Ingestion & Analysis  
- Detection Engineering  
- Security Event Investigation  
- Linux Administration  
- Honeypot Deployment  
- Troubleshooting & Debugging  

---

## 🚧 Status
- Architecture designed  
- SIEM deployed and configured  
- Honeypot operational  
- Log ingestion validated  
- Detection rules implemented  
- Alerts successfully generated  
