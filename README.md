# Enterprise Hybrid IT Support & Identity Management Lab

## Project Overview
This repository documents a fully functional, production-grade IT infrastructure portfolio simulating an enterprise hybrid operational environment. The lab bridges the gap between local automation engines and cloud directory services, paired with an industry-standard IT Service Management (ITSM) ticketing framework. 

The project is structured into two core operational phases:
1.  **Phase 1: Automated Identity Management (IAM)** – An API-driven automation pipeline that silently and securely provisions bulk user lifecycles from an on-premises flat-file database directly into Microsoft Entra ID using PowerShell and the Microsoft Graph SDK.
2.  **Phase 2: Help Desk Queue Architecture (ITSM)** – An enterprise service desk engine configured in Jira Service Management to log, manage, and resolve incoming Tier-1 incidents and structured Tier-2 technical escalations.

---

## Tech Stack & Core Concepts
* **Cloud Directory & Security:** Microsoft Entra ID (Azure AD), OAuth 2.0, RBAC, Service Principals
* **Automation & Scripting:** Windows PowerShell 5.1+, Microsoft.Graph PowerShell SDK, Parameter Splatting
* **IT Service Management (ITSM):** Jira Service Management, ITIL Framework (Incidents, Service Requests, Escalation Matrices)
* **Hardware Architecture:** Local Windows 11 Sandbox environment virtualized via UTM on Apple Silicon (Mac M2)

---

## 📂 Repository Structure
```text
├── microsoft-entra-id        # 
├── 
