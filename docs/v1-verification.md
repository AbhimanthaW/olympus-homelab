---
layout: default
title: V1 verification | Project Olympus
---
# V1 evidence and limits

**Recorded at the close of the initial infrastructure build, 20 October 2026.**

This is a bounded acceptance record. It describes what was observed at the time of testing, not current live telemetry or a production-grade reliability claim.

| Area | Verified at the V1 checkpoint | Not established |
| --- | --- | --- |
| OS deployment | ATLAS and HERMES independently booted Debian 13 | Continuous availability |
| Administration | MacBook SSH key access and Cockpit via SSH tunnels on both nodes | Full effective authentication and network exposure audit |
| Restart / outage | Controlled reboots; after a separate outage and manual restart both nodes had writable roots, working remote access and no failed services | Automatic restart when power returns; exhaustive data-integrity recovery |
| Storage | Short SMART self-tests completed without error | Complete surface/long-term reliability guarantee |
| Backup | Successful manually initiated, selected-file pulls from both nodes | Automatic schedule, comprehensive coverage, second backup location or bare-metal rebuild |
| Restore | Isolated file-copy/hash comparisons and a restored Python script copy | Full live workload/system restore |
| Athena | An ad hoc, small synthetic Python language-model calculation on HERMES, JSON output and retrieval | An always-on worker, scientific benchmark or realistic performance evaluation |
| Aula | Relevant source/tests inspected on the MacBook | Passing local test baseline or an executed Olympus Aula test |

## Known limitations

**ATLAS wireless:** intermittent packet loss was recorded in short tests; the later, smaller observed loss does not prove a permanent fix. Further stability assessment is needed before depending on it for unattended, latency-sensitive services.

**Security:** accessing Cockpit through a tunnel does not establish that its socket listens only on loopback. Password-login restrictions, effective firewall rules and router exposure were not comprehensively checked during closure.

**Backup coverage:** the tested workflow intentionally captures a selected list of files and scripts/results, not whole filesystems, all network/security settings or MacBook documentation. A separate recoverable copy of all important project data has not been demonstrated.

**Application onboarding:** initial Aula test preparation paused at a MacBook toolchain-resolution problem. The tests were not run on Olympus; the issue should not be described as an infrastructure failure or success.

## Publication evidence policy

The detailed engineering write-up will distinguish screenshots, terminal output and observed facts from intentions, estimates and later interpretations. Public artifacts are redacted and rewritten; raw internal inventory, keys, logs, private configuration and backup content are not published.

[Back to the project home](index.md)
