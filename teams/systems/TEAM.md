---
name: Systems
description: MasterClock semantics, service boundaries, and cross-domain persistence governance for RetroVue
slug: systems
manager: ../../agents/systems-architect/AGENTS.md
includes:
  - ../../agents/systems-architect/AGENTS.md
  - ../../agents/systems-lead/AGENTS.md
  - ../../agents/master-clock-engineer/AGENTS.md
  - ../../agents/service-boundary-engineer/AGENTS.md
  - ../../agents/persistence-governance-engineer/AGENTS.md
  - ../../agents/documentation-architect/AGENTS.md
  - ../../skills/architecture-decision/SKILL.md
  - ../../skills/code-review/SKILL.md
tags:
  - systems
  - architecture
  - retrovue
---

Systems maintains **one clock discipline** and **clear domain boundaries** across FastAPI and Postgres/SQLAlchemy, with **systems-lead** coordinating clock, API, persistence, and **documentation-architect** (cross-domain doc coherence) under **systems-architect**.
