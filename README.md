# Virtualization, Secure Operational Continuity and Risk Mitigation of a Legacy Healthcare System

## Purpose
This repository documents a legacy healthcare system risk mitigation and continuity initiative that I designed and implemented while working in a cardiology medical office.

The objective of this project was to preserve a mission-critical legacy healthcare application while reducing operational risk, improving recoverability, and containing cybersecurity exposure.

This repository contains **architecture and operations documentation**, not a tutorial or lab exercise.

---

## Background & Problem Statement

The medical office relied on a legacy healthcare application (**AdvantX 5.0**) backed by **Microsoft SQL Server 2008 R2**, running on **Windows 7 Pro SP1** physical hardware.

The system presented severe constraints:

- The application is **no longer vendor-supported**
- There is **no installer, setup media, or reinstall option**
- No additional licenses are available
- **Only one computer can use AdvantX at a time**
- Windows 7 is **end-of-life and unsupported**
- The system depended on one computer, so if it failed, everything stopped
- Application replacement or upgrade was not feasible

Because of these limits, using a **virtual machine** was the only way to keep the **system running**.

---

## System Overview

LEGACY SYSTEM (NO LONGER USED)
----------------------------------------------
PC A – Windows 7 (Physical)
  - AdvantX Medical Application
  - Microsoft SQL Server (Local)
    - Master Database
  - Printer: USB (direct)
  - LAN-restricted access only
  - Unsupported OS / No vendor support
  - No installer or setup media available
  - Single license (Only one computer may use AdvantX at a time) 
  - Retired from daily operations

PC B – Client Workstation
  - Client computer used only to access the application
  - No local database ownership
  - Dependent on PC A
  - LAN-restricted access only
  - Retired from daily operations


CURRENT PRODUCTION SYSTEM
-------------------------
PC C – Windows 11 Pro (Ethernet)
  - Oracle VirtualBox
    - Windows 7 VM
      - AdvantX Medical Application
      - Microsoft SQL Server (Local only)
      - Centralized production database
      - No internet browsing
      - LAN-restricted access only
      - Controlled printing path (USB via host)
  - Secure backups saved on an external SSD


CLIENT ACCESS
-------------
PC D – macOS (Wi-Fi)
  - Oracle VirtualBox
    - Windows 7 VM
      - AdvantX client access only
        - No local data storage
        - No database services installed
        - Users have limited access, only what is needed to do their job
        - Only one person can use the application at a time


EMERGENCY FALLBACK (OFFLINE ONLY)
---------------------------------
PC A + PC B
  - Powered off
  - Stored offline
  - Used only if VM recovery is not possible

---

## Why Virtualization Was the Only Viable Solution

Traditional solutions were not possible due to:
- No reinstall capability
- No vendor support
- No additional licenses
- Only one computer can use the application at a time
- Old hardware increased the risk of system failure

Virtualization allowed:
- Hardware independence
- Preservation of application behavior
- Centralized data control
- Rapid recovery from failure
- Reduced cybersecurity exposure

---

## Virtualization Platform Selection: Oracle VirtualBox

Oracle VirtualBox was selected because it:
- Supports legacy Windows operating systems reliably
- Accepts VHD disks created via Disk2VHD
- Runs on both Windows and macOS (Intel)
- Does not require proprietary licensing
- The system runs the old software in a stable and consistent way

The system runs only the AdvantX application and required services.

---

## Operational Model

- Only **one active AdvantX session** is allowed at any time
- All production data resides inside the Windows 7 VM on PC C
- Client systems store **no database or application data**
- Ethernet is preferred for the main system
- Wi-Fi is permitted for client access only
- Printing paths are controlled and predictable

This prevents:
- Data corruption
- Database divergence
- Licensing violations
- Concurrent write access

---

## Backup & Recovery

A simple and reliable backup model is used:
- Primary VM stored on PC C
- Secure backups saved on an external SSD
- Backups performed only when the VM is powered off

This ensures data consistency and protects against ransomware and hardware failure.

---

## Cybersecurity Considerations

- Windows 7 is an unsupported operating system and poses inherent risk
- Risk is **contained**, not ignored
- The legacy OS is isolated inside a virtual machine
- No internet browsing inside the VM
- No inbound network exposure
- Reduced attack surface compared to the original physical deployment

This design aligns with core security principles such as:
- Confidentiality
- Integrity
- Availability
- Least exposure
- Risk containment

This project does **not claim formal HIPAA compliance**, but demonstrates security-aware decision making appropriate for constrained healthcare environments.

---

## Upgrade & Future Flexibility

Because AdvantX and SQL data are encapsulated in a virtual machine:
- Hardware can be replaced without reinstalling the application
- Host operating systems can be upgraded independently
- Storage can be migrated easily
- Recovery time is significantly reduced

Virtualization separates **application lifecycle from hardware lifecycle**.

---

## Non-Goals

This project does not attempt to:
- Upgrade Windows 7 inside the VM
- Modify or patch AdvantX
- Replace vendor software
- Operate the live system in a cloud environment

Stability, continuity, and risk reduction were the priorities.

---

## Outcome

This project:
- No longer dependent on a single computer
- Reduced system failure and security risk
- Daily work continued without disruption
- Easier to recover after a problem
- Extended the life of the software

---

## Disclaimer

This repository contains **no PHI (Protected Health Information)**, no screenshots of patient data, and no configuration exports.  

All content is architectural and operational documentation only.
