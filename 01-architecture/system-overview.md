# System Overview

## Purpose
This document provides a high-level overview of the legacy healthcare system architecture currently in production.

## Context
This system supports a cardiology medical office using a legacy healthcare application (AdvantX) that cannot be reinstalled, upgraded, or relicensed.

## Architecture Summary
The legacy Windows 7 environment is encapsulated inside a virtual machine using Oracle VirtualBox, allowing hardware independence, risk containment, and improved recoverability.

---

## System Components

The system consists of four logical components with clearly defined roles:

- **PC A**: Original legacy production system, now reitred and retained offline for emergency fallback only.
- **PC B**: Legacy client workstation previously dependent on PC A, now retired.
- **PC C**: Primary production host running the legacy application inside a controlled virtualized environment.
- **PC D**: Client access system providing user interaction without local data storage or database services.

## Decision

The legacy AdvantX application and its Microsoft SQL Server database were encapsulated inside a Windows 7 virtual machine hosted on modern hardware.  

This virtual machine became the single production environment, replacing the original physical system while preserving application behavior and licensing constraints.

Client access was limited to controlled virtualized endpoints with no local data storage or database services.

---

## Justification

The original system could not be reinstalled, upgraded, or relicensed, and vendor support was no longer available.  
The entire application depended on a single physical computer, so if it failed, everything stopped.

Virtualization was the only viable way to reduce hardware failure risk while preserving a mission-critical healthcare application.

---

## Trade-offs

This design intentionally retains an unsupported operating system (Windows 7) inside a virtual machine.  
The system does not support horizontal scaling or multiple concurrent application instances due to licensing constraints.

Backups require planned downtime because the virtual machine must be powered off to ensure data consistency.

---

## Operational Impact

System recovery time was significantly reduced by decoupling the application from aging hardware.  
Daily operations became more predictable, with fewer interruptions caused by hardware instability.

Client systems no longer pose a data integrity or security risk, since all production data resides within the centralized virtual machine.

