# 🛡️ Home SOC Lab (Wazuh + Cowrie Honeypot)

## 📌 Objective
This project focuses on building a home SOC lab to simulate attacker activity and observe how it is captured, ingested, and analyzed within a SIEM. It highlights the end-to-end process of detection and basic security event investigation.

## 🧱 Tools Used
- Wazuh (SIEM / Log Analysis)
- Cowrie (SSH Honeypot)
- VirtualBox (Lab Environment)
- Linux (Ubuntu)

## 🏗️ Lab Setup
The lab was built using Oracle VM VirtualBox with multiple virtual machines to simulate a basic SOC environment. Wazuh was configured as the central SIEM for log collection and analysis, while Cowrie was deployed as an SSH honeypot to capture and monitor attacker activity.

## 🎯 What I Did

- Set up a virtual SOC lab using Oracle VM VirtualBox  
- Installed and configured Wazuh for log monitoring and alerting  
- Simulated failed login attempts to generate authentication logs  
- Verified detection of suspicious activity in Wazuh  
- Deployed Cowrie honeypot to capture attacker interactions  
- Simulated attacker access via SSH and executed commands  
- Analyzed honeypot activity and alerts within the Wazuh dashboard  
---

## ⚙️ Implementation

### 1. Virtual Lab Setup
Created virtual machines in Oracle VM VirtualBox to build the SOC environment.

![VirtualBox Setup](screenshots/soc-lab-virtualbox-overview.png)

---

### 2. Wazuh Installation
Installed Wazuh using the official script and confirmed it was working through the dashboard.

![Wazuh Installation](screenshots/wazuh-installation.png)  
![Wazuh Dashboard](screenshots/wazuh-dashboard-initial.png)

---

### 3. Failed Login Simulation
Generated failed authentication attempts using the `su wazuh` command to simulate suspicious login behavior.

![Failed Login Attempts](screenshots/failed_su_authentication_attempts.png)

---

### 4. Detection in Wazuh
Observed that Wazuh detected the failed login attempts and generated alerts related to authentication failures.

![Wazuh Detection](screenshots/wazuh_failed_login_detection.png)

---

### 5. Cowrie Honeypot Setup
Configured and started the Cowrie SSH honeypot to capture attacker interactions.

![Cowrie Startup](screenshots/cowrie_honeypot_startup.png)

---

### 6. SSH Attack Simulation
Connected to the honeypot via SSH and executed commands to simulate attacker behavior.

Example commands used:
- ssh root@localhost -p 2222  
- whoami  

![SSH Attack](screenshots/cowrie_ssh_attack_simulation.png)

---

### 7. Wazuh Monitoring Honeypot Activity
Verified that Wazuh detected honeypot activity including login sessions and command execution.

![Wazuh Cowrie Detection](screenshots/wazuh_cowrie_activity_detection.png)

---

## 📊 Results
- Successfully generated failed login attempts and attacker activity  
- Verified that Wazuh detects authentication failures and session activity  
- Observed real-time alerts in the dashboard  
- Demonstrated a full attack → detection workflow  

---

## 📚 What I Learned
- How SIEM tools like Wazuh collect and analyze logs  
- How authentication failures appear in monitoring systems  
- How honeypots capture attacker behavior  
- How to correlate attacker actions with SIEM alerts  

---

## 🚀 Skills
- SIEM monitoring (Wazuh)  
- Log analysis and alert investigation  
- Linux command line usage  
- Honeypot deployment (Cowrie)  
- Basic threat detection  

---

## 🚧 Status
- Lab setup ✅  
- Wazuh configured ✅  
- Attack simulation completed ✅  
- Detection verified ✅  
