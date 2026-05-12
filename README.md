# Wazuh SIEM Lab – Automated Threat Detection & Response

A hands-on cybersecurity project demonstrating real-time threat detection, threat intelligence integration, and automated incident response using Wazuh.

---

## Overview

This project simulates an enterprise-grade **Security Information and Event Management (SIEM)** environment. It goes beyond traditional monitoring by implementing a **closed-loop security workflow**:

**Detection → Analysis → Enrichment → Automated Response**

The system detects file-based threats, validates them using external intelligence, and automatically removes malicious files in real time.

---

## Tech Stack

* Wazuh SIEM (Linux Virtual Appliance)
* VirusTotal API (Threat Intelligence)
* Python (Active Response Automation)
* PowerShell (Windows Administration)
* XML (Wazuh Configuration)
* Windows 11 & Kali Linux (Endpoints)

---

## Key Features

* Centralized log collection and monitoring
* File Integrity Monitoring (FIM) for real-time detection
* Integration with VirusTotal for malware verification
* Automated threat removal using Python scripts
* Cross-platform endpoint monitoring
* Scalable agent configuration using Wazuh groups

---

## Architecture Workflow

1. File is created in a monitored directory
2. Wazuh detects the change using FIM
3. File hash is sent to VirusTotal
4. If flagged as malicious → alert triggered (**Rule ID 87105**)
5. Active Response script executes
6. Malicious file is automatically deleted

---

## Screenshots

### 1. Environment Setup

#### Network Configuration

![Host-only Adapter](images/host-only-network-adapter.png)
![NAT Adapter](images/nat-network-adapter.png)
![Bridge Adapter](images/bridge-network-adapter.png)

#### Virtual Machine Setup

![ISO Setup](images/iso-image-into-the-vm.png)

#### Initial Access

![Wazuh Login](images/wazuh-login.png)
![Manager IP](images/identifying-managers-ip-address.png)
![PowerShell Access](images/wazuh-powershell-login.png)

---

### 2. Wazuh Deployment & Dashboard

![System Start](images/starting-the-system.png)
![Browser Access](images/accessing-wazuh-via-browser-using-the-identified-ip.png)
![Web GUI Login](images/wazuh-web-gui-login.png)
![Dashboard](images/wazuh-dashboard.png)

---

### 3. Agent Deployment

![Deploy Agent](images/deploying-new-window-agent.png)
![Agent Summary](images/agent-summary.png)

---

### 4. File Integrity Monitoring (FIM)

![Create Directory](images/creating-a-monitored-directory.png)
![Central Config](images/centralized-agent-configs.png)
![Add Directory](images/adding-the-directory-to-the-agent.png)

#### Attack Simulation

![Create File](images/creating-a-new-file-within-the-protected-directory.png)

#### Detection

![FIM Alert](images/file-integrity-alert.png)
![Alert Evidence](images/evidence-of-the-alert.png)

---

### 5. VirusTotal Integration

![Integration Block](images/virus-total-integration-method-block.png)
![Manager Config](images/configuring-manager-with-virus-total.png)

#### Malware Testing

![Download Malware](images/download-the-malware.png)
![FIM Malware Flag](images/fim-flag-on-the-malware.png)

#### Detection Events

![Event 1](images/event-malware-flag.png)
![Event 2](images/event-malware-flag-2.png)

#### Analysis

![Malware Document](images/document-of-the-malware.png)
![VirusTotal Report](images/the-virustotal-report.png)
![Rule ID](images/rule-of-id.png)

---

### 6. Active Response Automation

#### Setup

![jq Dependency](images/prerequisite-of-the-package-jq.png)
![Create Directory](images/creating-my-active-response-directory.png)
![Create Script](images/creating-a-notepad.png)
![Wazuh Script](images/the-wazuh-ar-script.png)

#### Configuration

![Implement Script](images/implementing-the-script.png)
![Permissions](images/giving-wazuh-access-to-the-script-using-permission.png)
![Directory Access](images/script-directory-access-to-wazuh.png)
![Script Linking](images/directing-wazuh-to-use-that-script.png)
![Config Changes](images/changes-on-ossec-config.png)
![Restart Manager](images/restarting-wazuh-manager.png)

---

### 7. Automated Response Testing

![Download Malware 1](images/downloading-the-malicious-file.png)
![Download Malware 2](images/downloading-the-malicious-file-2.png)
![Download Malware 3](images/downloading-the-malicious-file-3.png)

---

### 8. Logs & Analysis

![Rules Description](images/rules-description.png)
![Malware Details](images/malware-doc-detail.png)
![VirusTotal Rate](images/virus-total-rate-report.png)
![Full Log](images/full-log.png)

---

## Project Structure

```
wazuh-siem-lab/
├── README.md
├── report/
│   └── wazuh_report.md
├── images/

```

---

## How to Reproduce

1. Install Wazuh Manager (Virtual Appliance)
2. Deploy agent on Windows endpoint
3. Configure File Integrity Monitoring (FIM)
4. Integrate VirusTotal API in `ossec.conf`
5. Enable Active Response module
6. Deploy Python response script
7. Test using EICAR malware sample

---

## Full Report

For detailed implementation, configuration, and analysis:

--> `wazuh_report.md`

---

## Gained

* Practical SIEM deployment and configuration
* Event correlation and threat detection
* Integration of external threat intelligence
* Automation of incident response workflows
* Reduction of Mean Time to Respond (MTTR)

---

## Future Improvements

* Implement false positive filtering (whitelisting)
* Extend automation (IP blocking, account isolation)
* Secure API key storage
* Improve logging and auditing
* Develop custom detection rules

---

## Authored and implemented
Khalid Abdullahi

Cybersecurity Student | SIEM & Automation Enthusiast
