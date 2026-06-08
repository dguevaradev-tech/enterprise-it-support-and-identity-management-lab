# Engineering & Troubleshooting Documentation: Cloud Provisioning Pipeline

## 📊 Project Evolution Overview
This document chronicles the technical challenges, architectural pivots, and security considerations encountered during the development of the **Entra ID Automated User Provisioning Engine**. The project evolved from a standard human-interactive script into a hardened, non-interactive enterprise API data pipeline.

---

## 🔍 Phase 1: The Multi-Tenant Handshake Failure
### The Approach
The initial plan utilized standard interactive device code authentication (`Connect-MgGraph -UseDeviceAuthentication`) without explicitly scoping a target directory backend, assuming the administrator account would natively route to its home environment.

### Why it Failed
The terminal threw authentication error **`AADSTS50020`**. Because the master root account was an external personal account (`outlook.com`) acting as a guest creator in the target sandbox, Microsoft’s default multi-tenant endpoint could not determine which specific organizational directory database to bind the session token to.

### Security Implications
* **Risk Profile:** Low.
* **Analysis:** The failure was structural and routing-based rather than an exploit vector. However, relying on default open-ended endpoint routing violates the core cloud principle of **Explicit Verification**, as the script blindly trusts the identity provider to guess the destination directory.

### The Fix
The execution command was modified to hard-code the target directory environment explicitly:
```powershell
Connect-MgGraph -UseDeviceAuthentication -TenantId "dguevaratechoutlook.onmicrosoft.com"

