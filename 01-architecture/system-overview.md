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
