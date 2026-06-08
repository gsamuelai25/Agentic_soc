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

# 🏗️ Architectural Topology

The platform is deployed as a containerized security monitoring stack orchestrated through Docker Compose and interconnected via an isolated virtual network named **SockNet**.

```text
┌─────────────────────────────────────────────────────────────┐
│                   Host Ubuntu Workspace                     │
└───────────────────────┬─────────────────────────────────────┘
                        │
                        ▼
              ┌───────────────────┐
              │   SockNet Bridge  │
              │ (Isolated Network)│
              └─────────┬─────────┘
                        │
        ┌───────────────┴────────────────┐
        │                                │
        ▼                                ▼

┌─────────────────────┐      ┌─────────────────────┐
│ SIEM / XDR Tier     │      │ Orchestration Tier  │
└─────────┬───────────┘      └─────────┬───────────┘
          │                            │
          │                            ▼
          │                  ┌─────────────────────┐
          │                  │      n8n Engine     │
          │                  │     Port : 5678     │
          │                  └─────────────────────┘
          │
          ├───────────────────────────────────────────┐
          │                                           │
          ▼                                           ▼

┌─────────────────┐                       ┌─────────────────┐
│     Indexer     │                       │  Web Dashboard  │
│   Port : 9200   │                       │   Port : 443    │
└─────────────────┘                       └─────────────────┘

          │
          ▼

┌─────────────────┐
│     Manager     │
│ Telemetry Core  │
└─────────────────┘

          │
          ▼

┌─────────────────┐
│ Local Endpoint  │
│      Agent      │
└─────────────────┘
```


## Data Flow

```text
Endpoint Agent
      │
      ▼
   Manager
      │
      ▼
   Indexer
      │
      ▼
Web Dashboard

Manager ─────────► n8n Engine
                     │
                     ▼
            Automated Actions
```

1. **Wazuh Indexer (Port 9200):** Optimized analytics engine that indexes, structures, and archives highly granular cryptographic security alerts. The LLM interacts directly with this endpoint for data lookup.
2. **Wazuh Manager:** The centralized behavioral engine. It aggregates logs, monitors structural rootkits, maps baseline compliance, and evaluates system event triggers.
3. **Wazuh Dashboard (Port 443):** Enterprise UI web panel mapping unified trends, risk profiles, and historical anomalies.
4. **n8n Automation Engine (Port 5678):** The foundational runtime for our Agentic AI workflow. Acting as the system maestro, it couples incoming SIEM webhooks to localized or cloud-based Large Language Models (LLMs).

---

## ⚙️ System Requirements & Prerequisites
Before executing the initialization scripts, verify your workspace fulfills the following structural baselines:
* **Operating System:** Ubuntu Linux Virtual Machine (Bare-metal installation, VMware Workstation, or VirtualBox recommended).
* **Hardware Allocations:** Minimum **8 GB RAM** (16 GB Recommended) and **4 vCPUs** to sustain elastic JVM heap sizes utilized by the indexer.
* **Terminal Shell:** Fully updated system packages with standard utilities (`curl`, `wget`).

---

## 🚀 Step-by-Step Deployment Guide

### Phase 1: Repository Ingestion & Tooling Provision
Clone the configuration trees directly onto your desktop workspace and update your local access control policies.

```bash
# Update localized apt cache mirrors
sudo apt update && sudo apt upgrade -y

# Install Git version control if missing
sudo apt install git -y

# Clone the authoritative sandbox orchestration tree
git clone [https://github.com/gsamuelai25/Agentic_soc.git](https://github.com/gsamuelai25/Agentic_soc.git)
cd Agentic_soc
---
### Phase 2: Docker Engine Provisioning

If your Ubuntu distribution lacks container runtimes, initialize the installation sequence using the pre-configured deployment script:

Bash
# Grant execution permissions to the setup manifest
sudo chmod +x install-docker.sh

# Run the runtime engine installation script
./install-docker.sh

# Verify the localized Docker daemon status and version
docker --version
