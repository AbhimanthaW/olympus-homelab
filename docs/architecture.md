---
layout: default
title: Architecture | Project Olympus
---
# Olympus V1: architecture and specifications

**Baseline:** 20 October 2026.

![Technical architecture diagram of Project Olympus V1, showing a home Wi-Fi router, MacBook administration and backup client, and independent ATLAS and HERMES Debian nodes](assets/olympus-v1-architecture.svg)

[Open full-resolution architecture diagram](assets/olympus-v1-architecture.svg) · [SVG source](https://github.com/AbhimanthaW/olympus-homelab/blob/main/docs/assets/olympus-v1-architecture.svg)

## 1. Physical hardware and node identities

| Specification             | ATLAS                                                                             | HERMES                                                               | MacBook Pro (administration client)                                          |
| ------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Device                    | Late-2012 Intel Mac mini                                                          | Intel NUC5CPYH                                                       | 14-inch MacBook Pro                                                          |
| Hardware identification   | macOS-era **Macmini6,1**                                                          | Board identified as **NUC5CPYB**                                     | Apple M1 Pro                                                                 |
| CPU                       | Intel Core i5-3210M **¹**                                                         | Intel Celeron N3050 **¹**                                            | Apple M1 Pro **²**                                                           |
| Logical processors        | 4 observed via Cockpit                                                            | 2 observed via Cockpit                                               | Not independently enumerated in V1 server evidence                           |
| Memory                    | **3.7 GiB usable** (4 GB class)                                                   | **7.7 GiB usable** (8 GB class)                                      | **16 GB unified** **²**                                                      |
| Local storage             | 500 GB, 5400 rpm Hitachi/HGST Travelstar hard disk, **APPLE HDD HTS545050A7E362** | Earlier-recorded **128 GB Transcend SSD370S** **¹**                  | 1 TB internal SSD **²**                                                      |
| Root filesystem           | ext4 on installed internal disk; ~457 GiB filesystem                              | ext4; ~111 GiB root filesystem                                       | macOS development workstation; filesystem version not audited                |
| Available root capacity   | ~433 GiB at last observation                                                      | ~100 GiB at last observation                                         | Not remeasured in V1 evidence                                                |
| Swap                      | None configured at last check                                                     | ~6.1 GiB earlier observed **¹**                                      | Managed by macOS; not inspected                                              |
| Operating system          | **Debian GNU/Linux 13 (Trixie)**                                                  | **Debian GNU/Linux 13 (Trixie)**                                     | macOS; precise release not captured                                          |
| Last verified kernel      | **6.12.113+deb13-amd64**                                                          | **6.12.113+deb13-amd64**                                             | Not part of Debian node baseline                                             |
| Wireless adapter / driver | Broadcom BCM4331, **b43**                                                         | Intel Wireless 3165, **iwlwifi**                                     | Client Wi-Fi; adapter details not audited                                    |
| Wired interface           | Ethernet available; not used as live V1 path                                      | Ethernet available; historical installation-sharing profile inactive | Not required for operating V1 topology                                       |
| Functional role           | Intended management, integration and lightweight shared services                  | Intended independent verification and background research            | Development, administration, heavier compute, artifact retrieval and backups |

## 2. Operating topology and network

All three computers operate on an **existing private home LAN**, using independent wireless connections in the final V1 topology. Server addressing came from DHCP; no static reservations were verified. The one-off direct Ethernet arrangement used during installation is **not** part of the final topology.

| Area | ATLAS | HERMES |
| --- | --- | --- |
| Network manager | NetworkManager for Wi-Fi | NetworkManager |
| Wireless interface | `wlp2s0b1` | `wlp2s0` |
| Driver and firmware | `b43`; firmware installed with `firmware-b43-installer` | `iwlwifi`; Intel firmware loaded |
| Wireless radio details | Broadcom BCM4331; observed 2.4 GHz channel 9 association | Intel Wireless 3165; working Wi-Fi association |
| Addressing | DHCP (not guaranteed stable) | DHCP (not guaranteed stable) |
| Known issue | Intermittent packet loss in short router-ping tests | No equivalent sustained throughput qualification established |
| Ethernet | `enp1s0f0`, managed separately from Wi-Fi | `enp3s0`; inactive historical profiles retained |

## 3. Installed system and operational mechanisms

| Mechanism | ATLAS | HERMES | Verification boundary |
| --- | --- | --- | --- |
| SSH | Available and authenticated via MacBook-held administrative key | Same | Login tested, but final password/root policy not fully audited |
| Cockpit | Active socket; dashboard used via SSH tunnel | Same | Tunnel access is **not** proof of local-only server-side listening |
| NetworkManager | Operational, including working DNS after reboot | Operational | ATLAS packet loss remains unresolved |
| Security updates | Periodic APT settings present | Settings present; manual upgrades and subsequent new-kernel boot observed | No continuous unattended-update and alerting audit |
| Disk checks | SMART overall and short self-test passed | Overall and short self-test passed | Short tests are not full lifetime or media guarantees |
| Python | `/usr/bin/python3` present | Python **3.13.5** used in synthetic experiment | Does not imply all scientific dependencies are installed |
| Node.js / Docker | Not found in PATH during previous runtime check | Final installation state not comprehensively audited | **Not** proven as operational V1 workloads |
| Project timers or orchestrator | None demonstrated | None demonstrated | No distributed scheduler and no scheduled Athena worker |

## 4. Execution, administration and backup data flows

**Administration:** MacBook SSH key → either Debian node, with Cockpit used through individual client-side SSH tunnels. Neither Debian node requires the other to boot or run its installed operating system.

**Research smoke path (verified once):** a small, local synthetic Python language-model calculation executed on **HERMES**, wrote a JSON result, and that result was retrieved to the MacBook. This was an ad hoc test.

**Backup (verified):** the MacBook manually initiates SSH reads and rsync selected-file pulls from ATLAS and HERMES into local dated snapshots. Config/inventory selections and project scripts/results were captured, with isolated file-level hash and copy comparisons performed. The workflow is neither scheduled nor a coherent transactional snapshot and does not support full bare-metal restoration.

## 5. Reliability, security and intended next workloads

- A controlled reboot and limited recovery following a real power outage were observed on both nodes, after **manual** power-on. Auto-start on AC restoration, unattended recovery and comprehensive data integrity have not been demonstrated.
- ATLAS's wireless packet loss has not been conclusively diagnosed. Neither node has a validated workload throughput, power-use or sustained-availability specification.
- SSH and Cockpit were accessed privately during setup, but the effective listener/firewall/router exposure configuration needs a final audit before introducing off-site access.
- **Aula** synthetic development tests and integration rehearsals are the highest-priority future applications; **no passing Aula workload was demonstrated on Olympus** at the V1 infrastructure milestone.
- **Athena** bounded research utilities are secondary; heavyweight inference remains on the MacBook unless specific measurements justify placement.
- Other NUCs/laptops and reserved future node names are **not active V1 infrastructure**. There is no shared filesystem, Kubernetes, pooled CPU/RAM or general cluster-wide job scheduler.

## 6. Publication and reproducibility boundaries

This page is a **sanitized, retrospective hardware and infrastructure snapshot**, not live system documentation. Its qualified device labels and observed metrics originate from the October 20 V1 closure, inventory, architecture and evidence records. The operational installation and troubleshooting case study is in preparation; the exact USB-less installation method must be reconstructed from primary logs before issuing a reproducible guide.

[Project home](index.md) · [V1 verification and known gaps](v1-verification.md) · [Repository](https://github.com/AbhimanthaW/olympus-homelab)
