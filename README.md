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
