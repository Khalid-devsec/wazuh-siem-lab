# Wazuh SIEM Lab: Automated Threat Detection and Response

## Introduction

This project demonstrates the deployment and configuration of a centralized **Security Information and Event Management (SIEM)** system using Wazuh. The objective was to design a security monitoring environment capable of not only detecting threats but also responding to them automatically.

The lab simulates a real-world enterprise security architecture by implementing a **defence-in-depth strategy**, integrating monitoring, threat intelligence, and automated response mechanisms.

By the end of the project, the system achieved a complete security workflow:

**Detection → Analysis → Enrichment → Automated Response**

---

## 2. Problem Statement

In modern IT environments, system logs are distributed across multiple endpoints (Windows, Linux, etc.), making it difficult to:

* Detect threats in real time
* Correlate security events
* Respond quickly to incidents

This lack of centralized visibility creates **security blind spots**, increasing the risk of undetected attacks such as:

* Unauthorized file modifications
* Malware execution
* Brute-force login attempts

Without a SIEM solution, organizations experience delayed detection and high **Mean Time to Respond (MTTR)**.

---

## Objectives

The main objectives of this project were:

* Deploy a centralized SIEM environment
* Configure endpoint monitoring using agents
* Implement File Integrity Monitoring (FIM)
* Integrate external threat intelligence using VirusTotal
* Automate incident response using Python scripts
* Reduce manual intervention in threat mitigation

---

## System Architecture

### Components

* **Wazuh Manager:** Central SIEM server (Linux-based)
* **Agents:** Windows 11 and Kali Linux endpoints
* **Threat Intelligence:** VirusTotal API
* **Automation:** Python Active Response Script

### Workflow

1. Endpoint generates an event (file creation/modification)
2. Wazuh agent sends logs to the Manager
3. FIM detects file changes
4. File hash is analyzed using VirusTotal
5. If malicious → alert triggered (Rule ID 87105)
6. Active response script deletes the file

---

## Implementation Phases

---

### Phase 1: Wazuh Deployment and Agent Integration

#### Overview

The Wazuh Manager was deployed as a virtual appliance using a pre-configured ISO. This ensured a stable and controlled environment for SIEM operations.

#### Key Steps

* Imported Wazuh virtual machine into VirtualBox
* Configured multiple network adapters (NAT, Host-only, Bridged)
* Identified Manager IP address using `ip a`
* Accessed Wazuh dashboard via web browser
* Installed and registered Windows agent using PowerShell

#### Outcome

* Successful connection between Manager and agent
* Centralized log collection established

#### Challenge

* Shell incompatibility (Bash vs PowerShell)

#### Resolution

Commands were executed in their appropriate environments:

* Bash → Linux (Manager)
* PowerShell → Windows (Agent)

---

### Phase 2: File Integrity Monitoring (FIM)

#### Objective

To monitor critical directories for unauthorized changes.

#### Implementation

* Created monitored directory:

  ```
  C:\temp\malware
  ```
* Configured FIM using centralized `agent.conf`
* Enabled syscheck module

#### Testing

* Created a file inside the monitored directory
* Verified alert generation in Wazuh dashboard

#### Outcome

Wazuh successfully detected:

* File creation events
* Timestamp and file path
* Associated user

#### Insight

At this stage, detection is **event-based**, meaning the system identifies changes but does not classify them as malicious.

---

### Phase 3: VirusTotal Integration

#### Objective

To enhance detection by verifying file reputation using external threat intelligence.

#### Implementation Steps

1. Registered for VirusTotal API key
2. Modified `ossec.conf` to include integration block
3. Linked integration to FIM events
4. Restarted Wazuh Manager

#### Testing

* Downloaded EICAR test malware file

#### Challenge

* Windows Defender quarantined the file before analysis

#### Resolution

* Added directory exclusion to allow file persistence

#### Results

* Wazuh enriched alerts with VirusTotal data
* High detection ratio confirmed malicious classification

#### Key Technical Insight

Wazuh uses Rule IDs to differentiate events:

* **550 / 554** → Normal file changes
* **87105** → Confirmed malicious file

This distinction ensures accurate and reliable automation in the next phase.

---

### Phase 4: Active Response Automation

#### Objective

To automatically remove malicious files upon detection.

#### Implementation

* Deployed Python-based active response script
* Installed required dependency (`jq`)
* Configured execution permissions
* Enabled Active Response module in Wazuh

#### Workflow

1. File is detected by FIM
2. VirusTotal confirms malicious status
3. Rule ID 87105 triggers
4. Python script executes
5. Malicious file is deleted

#### Testing

* Downloaded malware again to trigger response

#### Outcome

* File was deleted almost instantly
* Wazuh dashboard confirmed successful response

#### Impact

This significantly reduced **Mean Time to Respond (MTTR)** and demonstrated automated incident handling.

---

## Results and Analysis

The system successfully implemented a **closed-loop security model**:

* Detection via FIM
* Enrichment via VirusTotal
* Automated response via Python

### Key Achievements

* Real-time threat detection
* Accurate malware classification
* Immediate automated remediation
* Scalable configuration management

---

## Challenges and Solutions

| Challenge                  | Solution                                       |
| -------------------------- | ---------------------------------------------- |
| Shell compatibility issues | Used correct environments (Bash vs PowerShell) |
| Antivirus interference     | Added directory exclusion                      |
| Configuration errors       | Restarted Wazuh after changes                  |
| File detection timing      | Ensured persistence for hashing                |

---

## Limitations

* Potential false positives without filtering
* Dependence on external API (VirusTotal rate limits)
* Basic response action (file deletion only)

---

## Future Improvements

* Implement whitelisting to reduce false positives
* Extend automation (block IPs, disable accounts)
* Secure API key storage
* Improve logging and auditing
* Develop custom detection rules

---

## Finally

This project demonstrates how a SIEM platform such as Wazuh can evolve from a passive monitoring system into an **automated security enforcement solution**.

By integrating:

* File Integrity Monitoring
* External threat intelligence
* Active response automation

the system achieves a **proactive and secure posture**, capable of detecting and neutralizing threats in real time.

This implementation provides a strong foundation for advancing into full **Security Orchestration, Automation, and Response (SOAR)** environments.

---
