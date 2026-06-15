# Enterprise Hybrid IT Support, Automation & Governance Lab

## Project Overview
This comprehensive portfolio lab demonstrates the implementation, management, and troubleshooting of an enterprise hybrid IT service model. By bridging cloud-native identity directories with programmatic IT Service Management (ITSM) workflows, this project simulates a fast-paced corporate environment handling user lifecycle events, automated incident management, and cross-platform infrastructure diagnostics.

### Core Competencies Demonstrated:
* **Cloud Identity Governance:** Scripted user provisioning, attributes mapping, and access controls within Microsoft Entra ID.
* **API Integration & Automation:** Developing automated incident injectors utilizing PowerShell and Atlassian Jira Service Management REST APIs.
* **ITIL Operational Frameworks:** Managing end-to-end ticket lifecycles, asset tracking, and creating technical Knowledge Base (KB) playbooks.
* **Cross-Platform Diagnostics:** Triage of hardware, software, and networking faults across Windows, macOS, and Linux environments using CLI utilities.

---

## Technical Architecture & Environment
* **Hypervisor Layer:** VirtualBox / UTM (Emulating Windows 11 Enterprise workstations)
* **Identity Infrastructure:** Microsoft Entra ID (Cloud Identity Directory Sandbox)
* **ITSM Gateway:** Atlassian Jira Service Management (ITIL-Aligned Service Desk)
* **Automation Engine:** PowerShell 7.x (REST API Parsing & JSON Payload Architecture)

---

## Project Modules & Proof of Work

### 1. Cloud Identity Governance (Microsoft Entra ID)
To simulate rapid organizational onboarding, I engineered an automated user-provisioning solution. A custom PowerShell engine ingests corporate identity matrices to automatically map organizational units, build compliant User Principal Names (UPNs), assign department attributes (HR, Finance, Operations), and enforce temporary credential security boundaries.
* **Security Control Enforced:** Implemented immediate password rotation rules (`ForceChangePasswordNextSignIn = $true`) to protect accounts during the initial cloud onboarding phase.
* **Artifacts:** `scripts/ProvisionUsers.ps1` and verification captures inside `documentation/user-provisioning/`.

### 2. Programmatic Incident Ingestion (Jira Service Desk)
Rather than manually logging help desk issues, I built an automated incident injection system. This engine leverages PowerShell to convert simulated corporate hardware and software failures into JSON payloads, passing them securely through a Base64-authenticated Atlassian REST gateway.
* **Ticketing Lifecycle:** Managed incoming triaged alerts, applied custom metadata labels, and practiced enterprise workflows from Tier-1 intake up to formal Tier-2 engineering escalations.
* **Artifacts:** `scripts/InjectJiraTickets.ps1` and live portal dashboard screenshots in `documentation/jira-tickets/`.

### 3. Microsoft 365 Workspace Optimization (Knowledge Base)
To resolve recurring enterprise client disruptions, I authored a standardized internal knowledge base following professional ITIL documentation practices. These playbooks provide help desk personnel with clear, step-by-step Standard Operating Procedures (SOPs) to resolve profile corruptions and sync locks efficiently.
* **KB00142 (Outlook Remediation):** Safe mode troubleshooting, COM add-in isolation, profile rebuilding, and destructive `.ost` local cache pruning.
* **KB00195 (OneDrive Resets):** Purging expired generic items from Windows Credential Manager and executing backend `/reset` commands to force cloud re-indexing without data loss.
* **Artifacts:** Accessible markdown playbooks located in `/kb-articles/`.

### 4. Cross-Platform Diagnostics & Log Analysis
Simulating modern corporate offices running diverse systems, I compiled operational diagnostic logs to isolate network and hardware faults across Windows, macOS, and Linux clients using native command line interfaces (CLI).
* **Network Traces (`network-triage.log`):** Using `ping` and `traceroute` to isolate network drops beyond local gateways to edge firewall rule blocks.
* **Linux Kernel Triage (`linux-hardware-fault.log`):** Parsing `dmesg` ring buffers to capture physical sector I/O failures on raw storage devices (`/dev/sdb1`).
* **Windows System Analysis (`windows-event-critical.log`):** Extracting critical Event ID 41 (Kernel-Power) crash records from Event Viewer to trace system Blue Screens back to display driver timeouts (TDR Bugcheck 0x116).
* **Artifacts:** Active terminal outputs saved in `diagnostics/`.
---

## 📂 Repository Structure
```text
├── microsoft-entra-id                # Microsoft Entra ID Automated User Provisioning Engine
├── jira-integration                  # Programmatic Incident Ingestion & Service Desk Engine
├── kb-articles                       # ITIL-Aligned Internal Knowledge Base Documentation
├── cross-platform-diagnostics        # Heterogeneous OS Infrastructure Triage Records
