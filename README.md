# Building a Logical Diagram for Visualization

## Objective
To design a comprehensive logical architecture and backend workflow for the lab environment by mapping out all system components, data flows, and integration points. This will ensure clarity in how logs, alerts, and automation interact across tools like Splunk, Active Directory, Shuffle, and Slack—supporting effective detection, response, and analysis within a SOC-style setup.

## Tools Used 
- [Draw.io](https://app.diagrams.net/#G131nh-Co61dE6gBKoQ5e_8Wf64SdqlmpD#%7B%22pageId%22%3A%22JO1-W9AiMIgTA2bS2M9a%22%7D)


## 🔐 Active Directory Detection & Response Lab (Cloud-Based)

This lab is built using **[Vultr](https://www.vultr.com/)** a cloud hosting provider. The environment consists of the following **three servers**:

### 🖥️ Server Setup
1. **Windows Server (Domain Controller):**  
   - Promoted to a Domain Controller  
   - Active Directory installed and configured

2. **Windows Test Server:**  
   - Acts as the simulated victim machine

3. **Ubuntu Server (SIEM):**  
   - Hosts **Splunk**  
   - Collects telemetry and generates security alerts

---

### ⚠️ Threat Simulation
Outside the cloud environment, an **attacker machine (bad actor)** simulates an external threat. If the attacker scans the network and successfully authenticates to the test machine using valid credentials, the following sequence is triggered:

1. **Splunk Alert:**  
   - Triggered by telemetry detecting the unauthorized login

2. **Slack Notification:**  
   - Splunk sends an alert to Slack notifying of the incident

3. **Shuffle Automation (SOAR):**  
   - A pre-built playbook is triggered  
   - Sends an email to the SOC analyst asking:  
     _"Do you want to disable this user?"_

4. **SOC Analyst Response:**
   - If the response is **"No"** → no action is taken  
   - If the response is **"Yes"** →  
     - Shuffle instructs the **Domain Controller** to disable the user account  
     - A follow-up Slack message confirms:  
       _"Account `[username]` has been disabled."_

---

## Logical Architecture Diagram
![Active Directory Architecture Diagram](https://github.com/user-attachments/assets/b5e16be5-147e-46e2-9622-0fb8100b2a27)

