# System Overview

## Purpose
This document provides a high-level overview of the legacy healthcare system architecture currently in production.

## Context
This system supports a cardiology medical office using a legacy healthcare application (AdvantX) that cannot be reinstalled, upgraded, or relicensed.

## Architecture Summary
The legacy Windows 7 environment is encapsulated inside a virtual machine using Oracle VirtualBox, allowing hardware independence, risk containment, and improved recoverability.
