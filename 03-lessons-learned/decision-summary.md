# Architecture Decision Summary

## Overview

This document summarizes the key architectural decisions made during the virtualization and risk containment of a legacy healthcare application in a cardiology medical office environment.

The focus of these decisions was operational continuity, risk reduction, and recoverability under real-world constraints.

---

## Primary Constraints

The following constraints shaped all design decisions:

- Legacy healthcare application could not be reinstalled, upgraded, or relicensed
- Vendor support was no longer available
- The operating system (Windows 7) is end-of-life
- Only one application instance could run at any time
- The original system depended on one computer, so if it failed, everything stopped
- Clinical operations could not tolerate extended downtime

---

## Key Decisions

### 1. Virtualize Instead of Replace

The legacy application and database were encapsulated inside a Windows 7 virtual machine rather than attempting replacement or modernization.

**Reasoning:**
- Preserved application behavior and licensing constraints
- Eliminated dependency on aging physical hardware
- Enabled hardware independence and recovery flexibility

---

### 2. Treat the VM as an Application Appliance

The virtual machine is not used as a general-purpose workstation.

**Controls applied:**
- No internet browsing
- No email or third-party software
- Restricted network access
- Controlled USB and printing paths

This reduced exposure from an unsupported operating system.

---

### 3. Centralize All Production Data

All production data resides exclusively inside the primary virtual machine.

**Outcome:**
- Prevented data divergence
- Simplified backup and recovery
- Reduced risk from client endpoints

---

### 4. Offline Backup Strategy

Backups are performed offline using physically disconnected storage.

**Reasoning:**
- Prevents ransomware exposure
- Ensures data consistency
- Aligns with operational realities of the environment

---

## Accepted Trade-offs

The following trade-offs were intentionally accepted:

- Continued use of an unsupported operating system
- No horizontal scaling or high availability clustering
- Planned downtime required for backups
- Manual operational controls instead of automated tooling

These trade-offs were chosen to preserve stability and clinical continuity.

---

## Outcome

The final architecture:

- Eliminated dependence on a single computer
- Reduced operational and cybersecurity risk
- Enabled reliable recovery after failures
- Maintained critical clinical operations
- Extended the usable life of legacy healthcare software
