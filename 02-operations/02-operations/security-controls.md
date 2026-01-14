# Security Controls Overview

## Purpose
This document describes the security controls and risk containment measures applied to a virtualized legacy healthcare system operating in a cardiology medical office environment.

The objective is to reduce cybersecurity exposure while preserving the operation of a mission-critical legacy application that cannot be upgraded, reinstalled, or replaced.

---

## Threat Model

The primary risks addressed by this design include:

- Malware or ransomware infection
- Unauthorized access to legacy systems
- Data loss or corruption
- Hardware failure
- Vulnerabilities inherent to an unsupported operating system (Windows 7)

Because the legacy operating system cannot be patched or upgraded, risk mitigation focuses on **isolation and containment**, rather than complete risk elimination.

---

## Risk Containment Strategy

The legacy Windows 7 environment is fully encapsulated inside a virtual machine hosted on modern hardware.

This approach ensures:
- The legacy OS does not interact directly with modern endpoints
- Application behavior and licensing constraints remain unchanged
- Security exposure is limited to a clearly defined and controlled boundary

The virtual machine is treated as an **application appliance**, not a general-purpose workstation.

---

## Endpoint Restrictions

- The Windows 7 virtual machine is used exclusively to run the legacy healthcare application
- No internet browsing is permitted inside the VM
- No email clients or third-party software are installed
- USB access is restricted to controlled printing paths only

Client endpoints do not store application data or databases locally, reducing exposure and preventing data leakage.

---

## Network Restrictions

- The legacy VM operates with LAN-restricted access only
- No inbound connections from untrusted networks
- No public-facing services
- Network exposure is minimized to required application communication only

These controls significantly reduce the attack surface of the unsupported operating system.

---

## Access Controls

- Only authorized users can access the legacy application
- Client systems operate using reduced-privilege user accounts
- Administrative access is limited to system maintenance tasks
- Only one active application session is permitted at any time, enforcing both licensing and data integrity constraints

---

## Backup and Data Protection

- All production data resides exclusively inside the virtual machine
- Backups are performed offline using external storage
- Backup media is physically disconnected when not in use

This approach protects against ransomware, accidental deletion, and unauthorized access to backup data.

---

## Logging and Monitoring (Conceptual)

Due to application and platform limitations:

- Endpoint detection agents are not installed inside the legacy VM
- Monitoring focuses on host system stability, access control, and backup verification
- Operational awareness is maintained through administrative oversight rather than automated tooling

This reflects realistic constraints when operating unsupported legacy systems.

---

## CIA Triad Alignment

This security design aligns with core CIA triad principles:

- **Confidentiality**
  - Restricted network access
  - No internet browsing
  - No client-side data storage
  - Offline backups

- **Integrity**
  - Centralized production database
  - Controlled backup and recovery procedures
  - No concurrent write access

- **Availability**
  - Virtualization to remove hardware dependency
  - Predictable recovery through offline VM backups
  - Emergency fallback systems retained offline

---

## NIST Cybersecurity Framework Alignment (Conceptual)

This system reflects practical alignment with NIST Cybersecurity Framework functions:

- **Identify** – Risks, constraints, and legacy dependencies documented
- **Protect** – Isolation, access controls, and endpoint restrictions applied
- **Detect** – Operational awareness through controlled system behavior
- **Respond** – Documented recovery and restoration procedures
- **Recover** – Offline backups and hardware-independent restoration capability

This alignment represents risk-based decision making, not formal compliance certification.

---

## Limitations

- The legacy operating system remains unsupported
- No real-time threat detection inside the VM
- Security controls prioritize containment over modernization

These limitations were accepted to preserve application stability and clinical continuity.

---

## Outcome

This security design:
- Contains cybersecurity risk without disrupting clinical operations
- Reduces exposure of unsupported systems
- Prevents lateral movement from legacy environments
- Supports safe, predictable operation of a mission-critical healthcare application
