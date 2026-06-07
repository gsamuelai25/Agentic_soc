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

## Component Overview

| Component                | Purpose                                                                   |
| ------------------------ | ------------------------------------------------------------------------- |
| **SockNet**              | Internal isolated Docker network enabling secure container communication. |
| **Indexer**              | Stores and indexes security events, telemetry, and detection data.        |
| **Manager**              | Central analysis and correlation engine responsible for event processing. |
| **Web Dashboard**        | Administrative interface for monitoring, visualization, and management.   |
| **n8n Engine**           | Workflow orchestration platform used for automation and response actions. |
| **Local Endpoint Agent** | Collects endpoint telemetry and forwards data to the Manager.             |

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

## Network Design Principles

* Segmented architecture using an isolated Docker network (**SockNet**).
* Separation between monitoring infrastructure and automation services.
* Centralized telemetry ingestion through the Manager component.
* Secure web-based administration via the Dashboard.
* Extensible workflow automation through n8n integrations.
* Containerized deployment for portability and simplified operations.

```
```
