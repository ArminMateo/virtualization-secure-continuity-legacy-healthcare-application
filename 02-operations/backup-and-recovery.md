# Backup and Recovery Strategy

## Purpose

This document defines the backup and recovery strategy for the virtualized legacy healthcare system.

The objective is to ensure data integrity, rapid recovery from hardware failure, and protection against ransomware or accidental data loss while respecting application and licensing constraints.

---

## Scope

This strategy applies to:
- The Windows 7 virtual machine hosting AdvantX and Microsoft SQL Server
- Production data stored inside the VM
- Emergency fallback systems retained offline

It does not cover cloud backups or real-time replication.

---

## Backup Method

### Primary Backup Target
- Portable SSD storage device
- Physically disconnected when not in use
- Stored securely when offline

### Backup Type
- Full virtual machine backup
- Includes:
  - Operating system
  - AdvantX application
  - Microsoft SQL Server database
  - System configuration

---

## Backup Schedule

- **Frequency:** Weekly
- **Day:** Friday
- **Time:** After business hours

Backups are performed only when:
- The virtual machine is fully powered off
- No users are connected
- All database activity has stopped

This ensures database consistency and avoids corruption.

---

## Backup Procedure (High-Level)

1. Confirm no active AdvantX sessions
2. Shut down the Windows 7 virtual machine cleanly
3. Verify SQL Server services are stopped
4. Perform full VM backup to external drive
5. Verify backup completion
6. Safely disconnect and store backup media
7. Power on the virtual machine

---

## Retention Strategy

- Multiple backup versions retained
- At least one known-good backup kept offline
- Older backups rotated manually

---

## Recovery Strategy

### Primary Recovery Scenario
- Restore the virtual machine on the existing host
- Resume operations using the latest verified backup

### Alternate Recovery Scenario
- Restore the VM on different compatible hardware
- Oracle VirtualBox used to ensure hardware independence

### Emergency Fallback
- Physical legacy systems (PC A and PC B) remain powered off
- Used only if VM recovery is not possible

---

## Security Considerations

- Backups are stored offline to reduce ransomware risk
- No backups are exposed to the network
- Backup media is not left connected during normal operations

---

## Limitations

- Backups require planned downtime
- No live snapshots or replication
- Recovery depends on availability of compatible host hardware

These limitations were accepted to preserve application stability and data integrity.

---

## Outcome

This backup and recovery approach:
- Eliminates single points of failure
- Enables predictable recovery
- Protects against data loss and ransomware
- Supports long-term operational continuity
