# ICS Cyber Range  
## Behavior-Based Telemetry Analytics & Real-Time ICS Threat Detection

> Industrial Control System (ICS) Cybersecurity Research Platform focused on Modbus TCP threat detection, telemetry analytics, SIEM correlation, heatmap visualization, and CHAZOP-based cyber-physical analysis.

---

# Overview

The **ICS Cyber Range** is a high-fidelity Industrial Control System (ICS) security environment designed to simulate real-world Operational Technology (OT) infrastructures including:

- Dam Operations
- Electrical Substations
- Industrial Control Networks
- PLC-based Automation Systems
- Historian and Telemetry Pipelines

This project focuses on detecting stealthy and protocol-compliant cyber attacks targeting ICS environments using:

- **Snort IDS**
- **Wazuh SIEM**
- **pfSense Firewall**
- **Modbus TCP Inspection**
- **Behavior-Based Telemetry Analytics**
- **Heatmap Visualization**
- **MITRE ATT&CK for ICS Mapping**
- **CHAZOP (Cyber Hazard & Operability Analysis)**

The framework bridges the gap between:
- Packet-level intrusion detection
- Long-term telemetry monitoring
- Cyber-physical operational impact analysis

---

# Key Features

## Real-Time ICS Threat Detection
Detects malicious Modbus TCP traffic targeting PLCs using custom Snort signatures.

## Behavior-Based Analytics
Monitors communication behavior over time to identify:
- Low-and-slow attacks
- Abnormal command frequency
- Unauthorized writes
- Reconnaissance activity
- Traffic spikes

## Heatmap Visualization
Transforms telemetry into spatiotemporal heatmaps for:
- Anomaly identification
- Operational visibility
- Threat correlation

## SIEM Correlation
Wazuh aggregates and correlates:
- Snort IDS alerts
- Firewall telemetry
- Historian anomalies
- Attack frequency patterns

## MITRE ATT&CK for ICS Mapping
Every detected attack is mapped to:
- Tactics
- Techniques
- ICS adversarial behaviors

## CHAZOP Integration
Applies guideword-based cyber-operational hazard analysis across:
- PLCs
- HMIs
- Historians
- Communication Channels
- Engineering Workstations

---

# Architecture

## Network Segmentation

### IT / Corporate Network
`10.13.20.0/24`

### OT / Field Network
`10.14.6.0/24`

---

## Core Components

| Component | Purpose |
|---|---|
| Kali Linux | Attack Simulation |
| pfSense Firewall | IT/OT Segmentation |
| Snort IDS | Deep Packet Inspection |
| Wazuh SIEM | Alert Correlation |
| OpenPLC | Simulated PLC |
| Telegraf | Telemetry Collection |
| InfluxDB | Time-Series Historian |
| Grafana | Dashboards & Heatmaps |
| NGINX Reverse Proxy | Secure HMI Access |

---

# Detection Pipeline

```text
Attacker (mbpoll)
        ↓
Modbus TCP Traffic
        ↓
pfSense + Snort IDS
        ↓
Snort Alert Generated
        ↓
Syslog Forwarding (UDP 514)
        ↓
Wazuh Decoder
        ↓
Rule Correlation
        ↓
MITRE ATT&CK Mapping
        ↓
alerts.json + Dashboard Alert
```

---

# Attack Scenarios

## 1. FC03 Reconnaissance Attack

### Description
Performs Modbus register reads to enumerate:
- Process values
- PLC states
- Operational setpoints

### MITRE Mapping
- **Technique:** T0846
- **Name:** Remote System Discovery
- **Tactic:** Discovery

### Detection
- Rule ID: `100510`
- Severity: `Level 7`

---

## 2. FC06 Single Register Manipulation

### Description
Writes to a single PLC register to:
- Modify operational variables
- Test unauthorized access
- Perform stealthy process manipulation

### MITRE Mapping
- **Technique:** T0831
- **Name:** Manipulation of Control
- **Tactic:** Impair Process Control

### Detection
- Rule ID: `100502`
- Severity: `Level 10`

---

## 3. FC16 Multi-Register Attack

### Description
Simultaneously modifies multiple PLC registers:
- Water levels
- Setpoints
- Safety thresholds
- Process variables

### MITRE Mapping
- **Technique:** T0831
- **Name:** Manipulation of Control
- **Tactic:** Impair Process Control

### Detection
- Rule ID: `100501`
- Severity: `Level 12`

---

## 4. Modbus DoS Flood

### Description
Floods the PLC with high-frequency Modbus requests to:
- Exhaust buffers
- Delay legitimate commands
- Prevent operational response

### MITRE Mapping
- **Technique:** T0814
- **Name:** Denial of Service
- **Tactic:** Inhibit Response Function

### Detection
- Rule ID: `100530`
- Severity: `Level 13`

---

# Historian & Telemetry Pipeline

The telemetry framework continuously monitors ICS behavior using:

## Data Flow

```text
PLC
 ↓
Telegraf
 ↓
InfluxDB
 ↓
Grafana
 ↓
Heatmap Analytics
```

---

## Telemetry Collected

- Water Levels
- Flow Rates
- Register Values
- Communication Frequency
- Device Interactions
- Process Variables
- Write Command Activity

---

# Heatmap Analytics

Heatmaps provide:
- Communication intensity visualization
- Temporal anomaly detection
- Behavioral baselining
- Attack pattern visibility

## Benefits
- Reduces analyst cognitive load
- Improves anomaly detection
- Identifies stealthy reconnaissance
- Detects operational deviations

---

# CHAZOP Analysis

## Purpose

Cyber Hazard & Operability Analysis (CHAZOP) evaluates how cyber attacks impact physical operations.

---

## Guidewords Used

| Guideword | Meaning |
|---|---|
| MORE | Excessive activity |
| LESS | Missing telemetry |
| NO | Complete loss |
| OTHER THAN | Falsified behavior |
| AS WELL AS | Unauthorized additional actions |

---

## Critical Nodes Evaluated

- PLCs
- HMIs
- Firewalls
- Historians
- Communication Channels
- Engineering Workstations
- Reverse Proxy Infrastructure

---

# Reverse Proxy Architecture

NGINX was implemented as a Layer 4 TCP reverse proxy to securely expose OT HMI systems without direct IT-to-OT connectivity.

## Security Benefits

- Network Segmentation
- Controlled Access
- TLS Encryption
- Logging & Monitoring
- Reduced Attack Surface

---

# Technologies Used

## Security Stack
- Snort IDS
- Wazuh SIEM
- pfSense Firewall
- MITRE ATT&CK for ICS

## ICS Components
- OpenPLC
- Modbus TCP
- HMIs
- PLC Simulation

## Telemetry Stack
- Telegraf
- InfluxDB
- Grafana

## Infrastructure
- Ubuntu 22.04
- Kali Linux
- NGINX
- Virtualized OT Networks

---

# Results

| Metric | Result |
|---|---|
| Attack Scenarios Executed | 4 |
| Attacks Successfully Detected | 4 |
| Detection Rate | 100% |
| MITRE ICS Techniques Covered | 4 |
| Real-Time Alerting | Yes |
| Behavioral Analytics | Enabled |
| Heatmap Visualization | Enabled |

---

# Detection Improvements Achieved

## Before
- No protocol visibility
- No behavioral analysis
- No SIEM correlation
- No MITRE ICS context
- No frequency-based detection

## After
- Function-code-aware detection
- Real-time correlation
- Heatmap anomaly visualization
- MITRE ATT&CK integration
- Frequency-based DoS detection

---

# Research Contributions

This research contributes:

- A complete ICS detection pipeline
- Behavioral telemetry analytics for OT
- Heatmap-driven anomaly detection
- CHAZOP-integrated cyber analysis
- MITRE ATT&CK for ICS correlation
- Real-time Modbus threat detection

---

# Future Work

Future enhancements include:

- DNP3 protocol monitoring
- EtherNet/IP inspection
- Machine learning anomaly detection
- AI-driven telemetry analytics
- Automated incident response
- Expanded ATT&CK for ICS coverage
- Multi-site OT federation
- Advanced cyber-physical simulations

---

# MITRE ATT&CK for ICS Techniques Covered

| Technique ID | Technique |
|---|---|
| T0846 | Remote System Discovery |
| T0831 | Manipulation of Control |
| T0814 | Denial of Service |
| T0888 | Network Service Scanning |

---

# Academic Context

This project was developed as part of:

**Cybersecurity Capstone Project2**  
Pace University

Developed by:
- Jeytha Sahana Venkatesh Babu
- Jyothi Popuri
- Akash Pabshetwar

Instructor:
- Professor Joe Acampora

---

# Research Focus

This work focuses on improving:
- ICS Security Visibility
- OT Threat Detection
- Behavioral Monitoring
- Cyber-Physical Analysis
- Operational Stability
- Threat Correlation
- Telemetry Analytics

---

# References

This project is based on:
- MITRE ATT&CK for ICS
- Purdue Enterprise Reference Architecture
- Modbus TCP Security Research
- ICS Telemetry Analytics
- CHAZOP Methodology
- Industrial Threat Detection Research

---

# Citation

If referencing this project:

```text
Behavior-Based Telemetry Analytics and Heatmap-Driven Detection in the ICS Environment
CYB-691 Cybersecurity Capstone Project
Pace University
2026
```

---

---

# License

This repository is intended for:
- Academic Research
- Cybersecurity Education
- ICS Security Experimentation
- Defensive Security Research

Use responsibly and only in authorized environments.

------

## ❤️ Author

Created by **Jeytha Sahana** 

---
