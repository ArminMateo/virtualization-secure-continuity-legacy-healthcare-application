# Hardware Inventory

## Purpose
This document records the hardware platforms used across legacy, production, and client systems supporting the virtualized healthcare application environment.

The goal is to provide operational context, capacity awareness, and historical reference without impacting architectural clarity.

---

## PC A – Legacy Primary System (Retired)

**Role:**  
Original production system hosting AdvantX and Microsoft SQL Server.

**Status:**  
Retired from daily operations. Powered off and retained offline for emergency fallback only.

**Hardware Summary:**
- Model: Dell OptiPlex 7010
- Operating System: Windows 7 Professional SP1
- CPU: Intel Core i5-3470 (4 cores)
- Memory: 4 GB RAM
- Storage: 500 GB HDD
- Printer: USB (directly attached)

**Notes:**
- The original system depended on one computer, so if it failed, everything stopped
- Unsupported OS and application
- No reinstall or recovery path available

---

## PC B – Legacy Client Workstation (Retired)

**Role:**  
Client-only workstation dependent on PC A for application and database access.

**Status:**  
Retired from production. Powered off and retained offline for emergency fallback only.

**Hardware Summary:**
- Hardware class similar to PC A
- Operating System: Windows 7 Professional

**Notes:**
- No local database ownership
- Fully dependent on PC A during legacy operations

---

## PC C – Current Production Host (Primary System)

**Role:**  
Primary production host running the virtualized legacy environment.

**Status:**  
Active production system.

**Hardware Summary:**
- Model: HP EliteStudio 8 All-in-One G1 (27")
- Operating System: Windows 11 Pro
- CPU: Intel Core Ultra 7 265 (20 cores / 20 threads)
- Memory: 32 GB DDR5
- Storage: 1 TB NVMe SSD
- Network: Wired Ethernet

**Virtualization:**
- Oracle VirtualBox
- Hosts Windows 7 VM containing:
  - AdvantX Medical Application
  - Microsoft SQL Server (local only)
  - Centralized production database

**Notes:**
- No internet browsing inside the VM
- USB-controlled printing via host
- Secure offline VM backups stored on external drive

---

## PC D – Client Access System

**Role:**  
Client access endpoint for AdvantX.

**Status:**  
Active client system.

**Hardware Summary:**
- Model: MacBook Pro 16-inch (2019)
- Operating System: macOS (Intel)
- CPU: Intel Core i9 (8-core)
- Memory: 16 GB RAM
- Network: Wi-Fi

**Virtualization:**
- Oracle VirtualBox
- Windows 7 VM for client access only

**Restrictions:**
- No local data storage
- No database services installed
- Reduced-privilege user access
- Single active AdvantX session enforced
