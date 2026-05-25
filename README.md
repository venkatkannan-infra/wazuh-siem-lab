# 🛡️ SIEM Lab Project — Wazuh Home Lab

> A hands-on Security Information and Event Management (SIEM) lab built to simulate, detect, and analyze real-world cyber threats using Wazuh on a Windows environment.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Lab Architecture](#lab-architecture)
- [Tools & Technologies](#tools--technologies)
- [Lab Setup](#lab-setup)
- [Attack Simulations & Detections](#attack-simulations--detections)
- [Key Findings](#key-findings)
- [Screenshots](#screenshots)
- [Skills Demonstrated](#skills-demonstrated)
- [References](#references)

---

## Overview

This project documents the setup and use of a home SIEM lab using **Wazuh** — an open-source security monitoring platform. The goal was to:

- Deploy a fully functional SIEM environment at zero cost
- Monitor a live Windows endpoint for security events
- Simulate real-world attacks and observe how the SIEM detects them
- Analyze alerts and map them to the **MITRE ATT&CK** framework
- Document findings in a format suitable for a SOC analyst portfolio

---

## Lab Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Home Lab Environment                │
│                                                     │
│  ┌──────────────────┐      ┌─────────────────────┐  │
│  │  Windows 11 PC   │      │   Wazuh Server OVA  │  │
│  │  (Monitored      │◄────►│   (SIEM Platform)   │  │
│  │   Endpoint)      │      │   VirtualBox VM     │  │
│  │                  │      │                     │  │
│  │  Wazuh Agent     │      │  - Wazuh Manager    │  │
│  │  Installed       │      │  - Wazuh Dashboard  │  │
│  └──────────────────┘      │  - Elasticsearch    │  │
│                            │  - Kibana           │  │
│                            └─────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

---

## Tools & Technologies

| Tool | Version | Purpose |
|---|---|---|
| **Wazuh** | 4.14.5 | SIEM Platform — log collection, analysis, alerting |
| **VirtualBox** | Latest | Virtualization — runs Wazuh server as a VM |
| **Wazuh Agent** | 4.14.5 | Installed on Windows PC to ship logs to Wazuh |
| **Windows 11** | Latest | Monitored endpoint (attack target) |
| **MITRE ATT&CK** | v14 | Threat framework for mapping detections |

---

## Lab Setup

### Step 1 — Deployed Wazuh OVA in VirtualBox
- Downloaded the Wazuh OVA virtual machine from the official Wazuh website
- Imported the OVA into Oracle VirtualBox
- Configured VM with 4GB RAM for stable performance
- Accessed the Wazuh dashboard via browser at the VM's local IP address

### Step 2 — Deployed Wazuh Agent on Windows PC
- Used the Wazuh dashboard to generate a Windows agent installer command
- Ran the PowerShell installer as Administrator on the Windows endpoint
- Verified the agent appeared as **Active** in the Wazuh dashboard

### Step 3 — Verified Log Ingestion
- Confirmed Windows Security, System, and Application logs were flowing into Wazuh
- Observed baseline alerts from normal Windows activity (355 medium, 162 low severity)

---

## Attack Simulations & Detections

### 🔴 Simulation 1 — Brute Force / Authentication Failure

**Objective:** Simulate a brute force login attack and verify detection by the SIEM.

**Method:**
- Locked the Windows PC and intentionally entered incorrect passwords multiple times
- Monitored the Wazuh Threat Hunting dashboard for authentication failure alerts

**Result:**
- Wazuh detected **6 Authentication Failure** events
- Alerts were correctly tagged with `authentication_failed`, `windows`, and `windows_security`
- Events logged with accurate timestamps

**MITRE ATT&CK Mapping:**

| Tactic | Technique | ID |
|---|---|---|
| Credential Access | Brute Force | T1110 |

**Alert Severity:** Medium

---

### 🟡 Simulation 2 — Suspicious File Creation *(Coming Soon)*

**Objective:** Create a suspicious executable file and detect it via file integrity monitoring.

**Method:**
- Create a `.exe` file in a sensitive directory using PowerShell
- Monitor Wazuh File Integrity Monitoring (FIM) alerts

**Status:** 🔄 In Progress

---

### 🟡 Simulation 3 — New User Account Creation *(Coming Soon)*

**Objective:** Simulate insider threat by creating an unauthorized user account.

**Method:**
- Use `net user` command to create a new Windows user
- Detect and alert on account creation event

**Status:** 🔄 In Progress

---

## Key Findings

| # | Finding | Severity | MITRE Technique | Status |
|---|---|---|---|---|
| 1 | 6 Authentication failure events detected after brute force simulation | Medium | T1110 — Brute Force | ✅ Detected |
| 2 | 355 medium severity alerts from baseline Windows activity | Medium | Various | ✅ Monitored |
| 3 | 162 low severity alerts from normal system operations | Low | Various | ✅ Monitored |
| 4 | Windows Security logs successfully ingested in real time | Info | — | ✅ Confirmed |

---

## Screenshots

> Screenshots will be added to the `/screenshots` folder in this repository.

| Screenshot | Description |
|---|---|
| `dashboard-overview.png` | Wazuh Overview showing active agent and 24-hour alerts |
| `authentication-failure.png` | Threat Hunting view showing 6 brute force login detections |
| `agent-connected.png` | Windows PC showing as active monitored agent |
| `mitre-attack.png` | MITRE ATT&CK heatmap from the lab |

---

## Skills Demonstrated

- ✅ **SIEM Deployment** — Set up and configured Wazuh from scratch
- ✅ **Endpoint Monitoring** — Deployed and managed a Wazuh agent on Windows
- ✅ **Threat Detection** — Identified and analyzed real security alerts
- ✅ **Attack Simulation** — Simulated brute force and monitored results
- ✅ **MITRE ATT&CK** — Mapped detected events to the ATT&CK framework
- ✅ **Log Analysis** — Investigated Windows Security event logs
- ✅ **Incident Investigation** — Drilled into individual alerts for root cause
- ✅ **Documentation** — Recorded findings in a professional SOC-style format

---

## References

- [Wazuh Official Documentation](https://documentation.wazuh.com)
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [VirtualBox Downloads](https://www.virtualbox.org)
- [Windows Security Event IDs](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/)

---

## 👤 Author
Venkat Kannan
- 🌐 Portfolio: www.venkatkannan.com
- 💼 LinkedIn: [linkedin.com/in/venkan]
- 🐙 GitHub: [github.com/venkatkannan-infra]

---

> ⚠️ *This lab is for educational purposes only. All simulations were conducted in a controlled home lab environment on personally owned devices.*
