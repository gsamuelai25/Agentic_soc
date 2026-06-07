# 🛡️ Enterprise Autonomous SOC Lab: Wazuh SIEM & n8n Agentic AI Integration

[![Infrastructure](https://img.shields.io/badge/Infrastructure-Docker_Containers-blue?logo=docker)](https://www.docker.com/)
[![SIEM/XDR](https://img.shields.io/badge/SIEM%2FXDR-Wazuh_v4.x-orange?logo=wazuh)](https://wazuh.com/)
[![Automation](https://img.shields.io/badge/Automation-n8n_Agentic_AI-red?logo=n8n)](https://n8n.io/)
[![Target OS](https://img.shields.io/badge/Target_OS-Ubuntu_22.04+/24.04_LTS-E95420?logo=ubuntu)](https://ubuntu.com/)

## 📝 Course Overview & Objective
Welcome to Master Class on **Agentic AI inside Cyber Security Operations (SOC)**. 

Modern Security Operations Centers are chronically overwhelmed by high alert volumes and cognitive fatigue. The objective of this sandbox environment is to demonstrate how security engineering teams can deploy **low-to-no-cost autonomous orchestration tiers** to scale incident triage, analyze security telemetry, and execute self-healing playbook mitigations without expanding capital expenditure.

This repository orchestrates a completely localized, containerized **SIEM (Wazuh)** and an **Agentic Workflow Engine (n8n)** running on a dedicated virtualized network interface.

---

## 🏗️ Architectural Topology
The environment initializes a multi-container stack orchestrated via Docker Compose over an isolated network abstraction layer named `SockNet`.
[ Host Ubuntu Workspace ]
                            |
      +---------------------+---------------------+
      | (SIEM / XDR Aggregator Tier)              | (Orchestration Tier)
      |                                           |
[SockNet Bridge]                            [SockNet Bridge]
      |                                           |
+-----+-----+-----------------------+             |
|           |                       |             |
[Indexer]   [Manager]   [Web Dashboard] |          [n8n Engine]
(Port 9200) (Telemetry)   (Port 443)    |          (Port 5678)
|
[Local Endpoint Agent]
