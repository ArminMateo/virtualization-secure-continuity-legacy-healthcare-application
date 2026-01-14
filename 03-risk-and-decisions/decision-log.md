# Architecture Decisions & Risk Management

## Purpose
This document records key architectural decisions made to preserve a mission-critical legacy healthcare system under severe technical and operational constraints.

The goal was to reduce operational risk while maintaining system stability and clinical continuity.

---

## Key Constraints
The following constraints directly influenced all design decisions:

- Legacy application cannot be reinstalled, upgraded, or relicensed
- Vendor support is no longer available
- Operating system (Windows 7) is end-of-life
- Only one active application instance is permitted
- Clinical operations depend on system availability

---

## Virtualize the Legacy System

**Decision:**  
Encapsulate the legacy Windows 7 environment inside a virtual machine hosted on modern hardware.

**Rationale:**  
This was the only viable approach to reduce hardware failure risk while preserving application behavior and licensing constraints.

**Trade-offs Accepted:**
- Unsupported operating system retained
- No horizontal scaling
- Planned downtime required for backups

---

## Centralize All Production Data

**Decision:**  
All production data resides inside a single controlled virtual machine.

**Rationale:**  
This prevents data divergence, corruption, and unauthorized access from client systems.

**Risk Mitigated:**
- Data inconsistency
- Concurrent write conflicts
- Client-side data leakage

---

## Offline Backup Strategy

**Decision:**  
Use full offline VM backups stored on external SSD.

**Rationale:**  
Legacy system limitations prevent live snapshots or replication.

**Risk Mitigated:**
- Ransomware
- Accidental deletion
- Hardware failure

---

## Retain Physical Systems as Emergency Fallback

**Decision:**  
Keep original physical systems powered off and stored offline.

**Rationale:**  
Provides last-resort recovery if virtualization becomes unavailable.

**Risk Mitigated:**
- Total system loss
- Unrecoverable VM failure
