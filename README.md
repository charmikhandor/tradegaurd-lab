# TradeGuard Lab

**Goal:** build an instrumented mini trading-firm network (Ubuntu collector, Windows AD, clients, vulnerable web server) to demonstrate compromise → detection → automated containment.

This repository contains the skeleton for TradeGuard Lab: a reproducible, documented home lab that shows real-world incident scenarios, telemetry collection, detection rules, and automated containment. The project is designed to be safe (host-only), repeatable, and interview/demo friendly.

---

## Repository layout

tradeguard-lab/
├─ README.md
├─ ARCHITECTURE.md
├─ infra/ # IaC (Vagrant/Ansible) stubs & scripts
├─ kibana/ # exported dashboards & queries
├─ detections/ # rule files & notes (Suricata, Elastic queries, etc.)
├─ automation/ # containment scripts (python/bash) with --dry-run
├─ demo/ # demo screencast + artifacts (pcap snippets, timeline)
└─ SAFE-LABS.md # lab safety rules and kill-switch instructions


---

## Quickstart (high level)

1. Read `SAFE-LABS.md` and ensure **host-only** networking is enabled for the lab.  
2. Prepare your host machine (enable virtualization in BIOS, create `~/tradeguard-lab/vms`).  
3. Install VirtualBox + Extension Pack and confirm a Host-Only adapter exists.  
4. Download required ISOs/OVAs and place them in `infra/isos/` (see `infra/isos.txt` for filenames and checksums).  
5. Provision the core VMs manually or with the tooling in `infra/` (suggested VMs: `DC-WS2019`, `WIN10-TRADER1`, `UBU-SIEM`, `KALI-ATTACK`, `MRROBOT`).  
6. Install and configure telemetry collectors on `UBU-SIEM` (Elastic/OpenSearch + Beats) and forward Windows logs.  
7. Run Attack Scenario 1 (recorded or live), observe alerts in dashboards, and test the automation scripts in `automation/`.

---

## Objectives & scope

- Simulate an identity-based attack in an Active Directory environment.
- Centralize telemetry: Windows events, file logs, network IDS (Suricata/Zeek).
- Create detection rules with low false-positive rates, validated against a “trading noise” generator.
- Implement simple automation (containment playbooks) that can disable AD accounts, block IPs, and quarantine shares.
- Produce an IR playbook, incident report, and reproducible artifacts for interview demos.

---

## Required downloads (store in `infra/isos/`)

- Ubuntu Server LTS ISO
- Windows Server 2019 ISO (evaluation)
- Windows 10 ISO (or installer)
- Kali Linux ISO or OVA
- Mr. Robot OVA (vulnerable target)

Record checksums and source URLs in `infra/isos.txt`.

---

## Minimal host requirements (adjust to your hardware)

- CPU: 4 cores (more recommended)
- RAM: 16 GB recommended (12 GB minimum workable)
- Disk: 200 GB free (SSD preferred)
- Virtualization: VT-x / AMD-V enabled

---

## Safety & reproducibility

- **Always use host-only networks** for offensive testing. See `SAFE-LABS.md` for the full safety checklist.
- Create snapshots after clean OS installs.
- Each automation script must support `--dry-run` and verbose logging.
- Include a `kill-switch` in `infra/kill-switch.sh` to power off all lab VMs in an emergency.

---

## Deliverables (what to include in the final portfolio)

- Architecture diagram (SVG/PNG) in `ARCHITECTURE.md`.
- IaC stubs (Vagrantfile / Ansible playbooks) in `infra/`.
- Kibana/OpenSearch dashboard exports in `kibana/`.
- Detections and rationales in `detections/`.
- Automation scripts (safe, tested) in `automation/`.
- Short demo screencast + sample evidence (pcap, logs, timeline) in `demo/`.
- Incident report (one-page exec summary + technical timeline + remediation checklist).

---

## How I will structure commits

- `chore/infra` — VM provisioning and iso catalog
- `feat/telemetry` — collectors, dashboard exports
- `feat/detections` — detection rules and test logs
- `feat/automation` — containment scripts and tests
- `docs/*` — architecture, playbooks, SAFE-LABS

---

## Contact / Author
**Charmi Khandor** — ckhandor@andrew.cmu.edu


