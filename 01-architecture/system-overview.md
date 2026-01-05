# System Overview

## Purpose
This document provides a high-level overview of the legacy healthcare system architecture currently in production.

## Context
This system supports a cardiology medical office using a legacy healthcare application (AdvantX) that cannot be reinstalled, upgraded, or relicensed.

## Architecture Summary
The legacy Windows 7 environment is encapsulated inside a virtual machine using Oracle VirtualBox, allowing hardware independence, risk containment, and improved recoverability.

---

## Hardware Overview

### PC A – Legacy Primary System (Decommissioned)
- Model: Dell OptiPlex 7010
- Operating System: Windows 7 Professional SP1
- CPU: Intel Core i5-3470 (4 cores)
- Memory: 4 GB RAM
- Storage: 500 GB HDD
- Role:
  - Original AdvantX application host
  - Local Microsoft SQL Server
  - USB-connected printer
- Status: No longer used, powered off, retained for emergency fallback only

---

### PC B – Legacy Client Workstation (Decommissioned)
- Hardware Class: Same generation as PC A
- Operating System: Windows 7 Professional
- Role:
  - Client-only endpoint
  - Dependent on PC A for database access
- Status: Retired

---

### PC C – Current Production Host (Primary System)
- Model: HP EliteStudio 8 All-in-One G1 (27")
- Operating System: Windows 11 Pro
- CPU: Intel Core Ultra 7 265 (20 cores / 20 threads)
- Memory: 32 GB DDR5
- Storage: 1 TB NVMe SSD
- Network: Ethernet (primary)
- Role:
  - Oracle VirtualBox host
  - Runs Windows 7 VM containing:
    - AdvantX Medical Application
    - Microsoft SQL Server (local only)
    - Centralized production database
- Notes:
  - No internet browsing inside VM
  - Controlled USB printing via host
  - Secure offline VM backups stored on external drive

---

### PC D – Client Access System
- Model: MacBook Pro 16-inch (2019)
- Operating System: macOS (Intel)
- CPU: Intel Core i9 (8-core)
- Memory: 16 GB RAM
- Network: Wi-Fi
- Role:
  - Oracle VirtualBox host
  - Runs Windows 7 VM for AdvantX client access only
- Restrictions:
  - No local data storage
  - No database services installed
  - Reduced-privilege user access
  - Single active AdvantX session enforced
