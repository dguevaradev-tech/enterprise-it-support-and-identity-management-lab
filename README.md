# Entra ID Automated User Provisioning Engine

## Project Overview
This project demonstrates an enterprise-grade automation solution for provisioning user lifecycles inside Microsoft Entra ID (Azure Active Directory) using PowerShell and the Microsoft Graph API. It transitions away from buggy interactive user-login sessions by leveraging a **Service Principal Application Registration (Client Secret Auth)** to silently and securely stream bulk identities from an on-premises CSV flat-file directly into a cloud directory database.

## Tech Stack & Concepts
* **Cloud Platform:** Microsoft Entra ID (Azure AD)
* **Automation Engine:** Windows PowerShell (Microsoft.Graph Module)
* **Authentication Flow:** OAuth 2.0 Client Credentials Grant (App-Only Service Principal)
* **Advanced Scripting Techniques:** PowerShell Parameter Splatting, Advanced Error Handling, CSV Parsing Matrix

## Script Architecture & Design
To ensure robustness, the solution bypasses common legacy execution hurdles:
1.  **Elimination of WAM/Interactive Traps:** Uses a secure `PSCredential` object mapped to an enterprise App Registration to guarantee permanent, non-interactive connectivity.
2.  **Splatting over Backticks:** Eliminates parsing glitches (`PositionalParameterNotFound`) by packaging user parameters natively into robust hashtable dictionaries (`@UserParams`) before hitting the cloud endpoint API.

## Setup & Installation Instructions

1. **Prerequisites:**
   Ensure the Microsoft Graph PowerShell SDK is installed on your management endpoint:
   ```Powershell
   Install-Module Microsoft.Graph -Scope CurrentUser
