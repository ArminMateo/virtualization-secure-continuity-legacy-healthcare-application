# Security Controls Overview

## Purpose
This document describes the security controls and risk containment measures applied to the virtualized legacy healthcare system.

The objective is to reduce cybersecurity exposure while preserving the operation of a mission-critical legacy application that cannot be upgraded, reinstalled, or replaced.

---

## Threat Model

The primary risks addressed by this design include:

- Malware or ransomware infection
- Unauthorized access to legacy systems
- Data loss or corruption
- Hardware failure
- Unsupported operating system vulnerabilities

Because the legacy operating system cannot be patched or upgraded, risk mitigation focuses on isolation and containment rather than elimination.

---

## Risk Containment Strategy

The legacy Windows 7 environment is fully encapsulated inside a virtual machine.

This approach ensures:
- The legacy OS does not interact directly with modern endpoints
- Application behavior remains unchanged
- Security exposure is limited to a controlled boundary

The virtual machine is treated as an application appliance, not a general-purpose workstation.

---

## Endpoint Restrictions

- The Windows 7 virtual machine is used only to run the legacy application
- No internet browsing is permitted inside the VM
- No email clients or third-party software are installed
- USB access is limited to controlled printing paths only

Client endpoints do not store application data or databases locally.

---

## Network Restrictions

- The legacy VM operates with LAN-restricted access only
- No inbound connections from untrusted networks
- No public-facing services
- Network exposure is minimized to required application communication only

This reduces the attack surface of the unsupported operating system.

---

## Access Controls

- Only authorized users can access the legacy application
- Client systems operate with reduced-privilege user accounts
- Administrative access is limited to system maintenance only
- Only one active application session is permitted at any time, enforcing licensing and data integrity constraints

---

## Backup and Data Protection

- Production data resides exclusively inside the virtual machine
- Backups are performed offline using external storage
- Backup media is physically disconnected when not in use

This protects against ransomware, accidental deletion, and unauthorized access.

---

## Logging and Monitoring (Conceptual)

Due to application and platform limitations:
- Traditional endpoint detection agents are not installed inside the legacy VM
- Monitoring focuses on host system stability, access control, and backup verification
- Operational awareness is maintained through administrative oversight rather than automated tooling

---

## Limitations

- The legacy operating system remains unsupported
- No real-time threat detection inside the VM
- Security controls prioritize containment over modernization

These limitations were accepted to preserve application stability and operational continuity.

---

## Outcome

This security design:
- Contains risk without disrupting clinical operations
- Reduces exposure of unsupported systems
- Prevents lateral movement from legacy environments
- Aligns with real-world healthcare operational constraints
