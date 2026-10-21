# Project Olympus

**A private, two-node Linux homelab built from repurposed computers.**

[![Status: V1 infrastructure complete](https://img.shields.io/badge/V1%20infrastructure-complete-245b50?style=flat-square)](#v1-status)
[![Scope: private experimental lab](https://img.shields.io/badge/scope-private%20lab-45536a?style=flat-square)](#purpose-and-boundaries)

Project Olympus is an independent systems-engineering initiative for learning practical Linux administration, networking, debugging, automation, and operational recovery. Its purpose is to support **Project Aula** development verification and modest **Project Athena** research tasks.

**V1 infrastructure milestone closed: 20 October 2026.**
## Architecture at V1

| Component | Role | Observed foundation |
| --- | --- | --- |
| **ATLAS** | Repurposed late-2012 Intel Mac mini; intended integration and lightweight management | Debian 13, independent boot, private-LAN SSH and tunneled Cockpit administration |
| **HERMES** | Repurposed Intel NUC; intended verification and bounded background work | Debian 13, independent boot, private-LAN SSH, Cockpit and a synthetic Python/Athena smoke run |
| **MacBook Pro** | Development, administration, heavier computation and selected-file backup destination | SSH client, artifact retrieval and manually initiated backups |

Each server owns its CPU, memory and storage. The MacBook is **not** an always-on runtime dependency; it *is* needed for the current manual backup workflow. The operating topology uses the existing home LAN and independent Wi-Fi connections, without a distributed scheduler or shared filesystem.

See the [illustrated technical architecture and hardware specifications](docs/architecture.md).

## V1 status

**Verified at the dated checkpoint:**
- Debian 13 running on two independent nodes, with remote key-based administration and Cockpit access through SSH tunnels.
- Controlled restart and basic post-outage recovery checks: accessible systems, writable root filesystems and active administration services.
- Limited SMART short-test passes on both disks.
- A successful **manual, selected-file** off-node backup from both servers, plus isolated file-level integrity and restoration checks.
- One small **synthetic** Python calculation on HERMES, with result transfer to the MacBook.

Read the [V1 verification summary](docs/v1-verification.md) for the precise evidence boundaries.

## Purpose and boundaries

1. **Aula:** isolated development verification and synthetic-data testing.
2. **Athena:** bounded calculations, experiment preparation and reproducible artifacts; heavy model inference remains on the MacBook unless measured otherwise.
3. **Learning:** Linux, networking, systems engineering, security and recovery.
4. **Optional services:** only with explicit resource, security and cleanup plans.

This lab is private by design. **No Olympus management interface or service is being published by this repository or its future GitHub Pages site.**

## Publication

- [Public architecture overview](docs/architecture.md)
- [V1 verification and limitations](docs/v1-verification.md)
- **Full case study:** in preparation, with an emphasis on the USB-less installation path, firmware/DNS troubleshooting, outage recovery and verification.

The [GitHub Pages site](https://abhimanthaw.github.io/olympus-homelab/) hosts the public project documentation and is intended to become the canonical home of the forthcoming article. A later Medium cross-post and LinkedIn announcement are planned.

## Source and licensing

The public documentation is an original, curated account of a personal engineering project. **No reuse license has been granted at this stage**; examples and article licensing will be decided separately before release. Private operational records, credentials, logs and configurations are intentionally excluded.

> **Snapshot note:** statements above describe evidence recorded on **20 October 2026**, not live monitoring or a guarantee of present-day service health.
