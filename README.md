# SIM — Deterministic SOC State Engine

A deterministic, state-driven SOC incident engine built on top of Wazuh telemetry.

SIM ingests security events into structured state, correlates activity across time, maps MITRE ATT&CK techniques locally (offline), and manages incidents through controlled, rule-based lifecycle logic.

AI is used strictly as an interpretation layer — never as the source of security truth.

---

SIM treats incidents as stateful objects, not temporary alerts.


## Why SIM Exists

Most SOC workflows are dashboard-driven.

Dashboards are excellent for visibility.  
They are weak for maintaining structured, persistent state.

Alerts appear.
Analysts click.
Context lives in multiple places.

SIM treats security reasoning as a stateful system:

- Events are stored as structured data
- Incidents evolve through controlled lifecycle transitions
- Correlation operates across time windows
- MITRE mapping is deterministic and offline
- Decisions are auditable

The goal is simple:

> Reduce alert fatigue and make security reasoning reproducible.

---

## Core Capabilities

- Telemetry ingestion from Wazuh indexer
- Structured SQLite state (events, facts, incidents, decisions)
- Local MITRE ATT&CK v18.1 pinning (offline lookup)
- Time-window attack chain correlation
- Deterministic incident promotion
- Controlled state transitions (no duplicate open incidents)
- CLI and API interfaces
- AI-assisted triage explanations (non-authoritative)

---

## Architecture Overview

Wazuh Agents  
→ Wazuh Manager / Indexer  
→ SIM Ingestion Layer  
→ Structured State (SQLite)  
→ Correlation & Policy Engine  
→ Incident Lifecycle Management  
→ AI Interpretation Layer (optional)

Deterministic core first.  
Language model second.

---

## Design Principles

- Security truth must be deterministic
- State must be auditable and reproducible
- Rule-based logic precedes probabilistic AI
- Incident lifecycle must move forward consistently
- Separation between reasoning engine and language model

## System Boundaries

SIM is not:

- A SIEM replacement
- A log storage platform
- A probabilistic AI decision engine

SIM is:

- A deterministic reasoning layer
- A structured incident state manager
- A correlation and lifecycle control engine

---

## Project Structure
sim/
├── ingest/ # Telemetry ingestion (Wazuh indexer)
│ └── wazuh_indexer.py
├── state.py # Authoritative structured state management
├── incidents.py # Incident lifecycle & promotion logic
├── chains.py # Time-window attack chain correlation
├── policy.py # Rule-based decision logic
├── mitre.py # Local MITRE ATT&CK lookup & pinning
├── triage.py # Human-readable hypothesis generation
├── hypotheses.py # Structured reasoning primitives
├── db.py # SQLite schema & connection layer
├── models.py # Data models
├── cli.py # Command-line interface
├── api.py # API interface
└── llm.py # Optional AI interpretation layer

