# Windows Security Audit Framework
### Enterprise-Grade Security Auditing, Forensics, & Threat Hunting for Windows Environments

---

> ### Data Privacy & Verification Notice
> **Proprietary Codebase:** The complete source codebase for this project is hosted in a private repository to protect custom threat signatures, forensic modules, and system administration logic. 
> 
> **Live Verification:** This repository serves as the public system architecture map and technical documentation. I am highly comfortable performing a live, end-to-end system demonstration and code walk-through during an interview to verify all architectural implementations and logic flows.

---

## Executive Summary

The **Windows Security Audit Framework** is a comprehensive, PowerShell-based security auditing and threat-hunting engine equipped with a modern, responsive Web Dashboard. 

Designed to map live Windows system states to CIS Benchmarks, NIST, and POPIA (Protection of Personal Information Act) requirements, it performs deep forensic analysis and system integrity checks without requiring heavy third-party enterprise agents.

---

## Technical Architecture: Zero-Dependency API

A major architectural achievement of this framework is that it runs with **zero external server dependencies** (no IIS, Apache, or Node.js required). It hosts its backend API directly from a live PowerShell session.

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        WEB FRONTEND (HTML/JS)                          │
│     Built with Tailwind CSS — Responsive Dark/Light Mode adapt         │
└──────────────────────────────────▲─────────────────────────────────────┘
                                   │ HTTP / API polling (localhost:8080)
                                   ▼
┌────────────────────────────────────────────────────────────────────────┐
│                        BACKEND API (PowerShell)                        │
│   Hosts a local REST API directly via .NET's [HttpListener] class     │
│   Streams live audit findings to the frontend via WebSocket-like sync  │
└──────────────────────────────────▲─────────────────────────────────────┘
                                   │ Internal Jobs
                                   ▼
┌────────────────────────────────────────────────────────────────────────┐
│                       SECURITY AUDIT ENGINE                           │
│   Asynchronous job-polling scanning WMI, CIM, Registry, and Memory     │
└────────────────────────────────────────────────────────────────────────┘

 Core Diagnostic Capabilities

  - Deep Process Triage: Detects process injection, unsigned binaries running in
    memory, and fileless malware by scanning heuristic checks against CIM/WMI
    namespaces.
  - Persistence Hunting: Scans WMI subscriptions, Registry Autoruns, and Windows
    Scheduled Tasks for unauthorized backdoors.
  - Forensic Analysis: Audits browser extensions, local HOSTS file integrity,
    and recent system execution timelines.
  - Crypto Miner Detection: Identifies abnormal CPU usage patterns and known
    mining signatures.
  - System Hardening Audit: Inspects User Account Control (UAC), Secure Boot,
    TPM status, and Windows Defender active configurations against enterprise
    baselines.

 Scan Profiles & Execution Modes

The framework supports multiple tiered scanning modes depending on the incident
response requirement:

| Mode           | Duration  | Description                                                                     |
| -------------- | --------- | ------------------------------------------------------------------------------- |
| **⚡ Quick**    | 2-3 min   | Essential checks: Memory integrity, Disk Health, Critical System Files.         |
| **📋 Standard** | 5-7 min   | Core checks + full Persistence Hunting (Autoruns, WMI).                         |
| **🔍 Deep**     | 10-15 min | Comprehensive audit: Network, Firewall, Defender, and OS Hardening.             |
| **🔬 Forensic** | 20+ min   | Full investigation: Timeline analysis, verbose system logs, and threat hunting. |

🛠️ Technology Stack & Requirements

  - Backend Engine: Windows PowerShell 5.1+ (Leveraging .NET Framework)
  - Frontend UI: HTML5, modern JavaScript, Tailwind CSS
  - Reporting: Auto-generates beautifully formatted HTML, JSON (for machine
    readability/automation), and CSV reports.
  - OS Support: Windows 10 & Windows 11 environments.

Architected and maintained by Sandiso Mazibuko.
