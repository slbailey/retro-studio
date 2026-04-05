# RetroStudio

**RetroStudio** is the **Paperclip Agent Company** for **RetroVue**: a coordinated set of agent roles that **design, specify, and implement** a **simulated linear TV network** (scheduled playout, EPG semantics, master-reference timing). This repository holds **org definition only**—`COMPANY.md`, agents, teams, and skills—not the deployed RetroVue runtime by itself.

| | Repository | Purpose |
|---|------------|---------|
| **RetroVue** | [**github.com/slbailey/retrovue**](https://github.com/slbailey/retrovue) | FastAPI services, Postgres/SQLAlchemy, Playlog, ChannelManager, ProgramDirector, ffmpeg Producers, OverlayStages, infrastructure—**what runs** |
| **retro-studio (this repo)** | Agent company package | `COMPANY.md`, `agents/`, `teams/`, `skills/`—**who plans, reviews, and edits** RetroVue under shared rules |

Import **this** repo into [Paperclip](https://paperclip.ing) (or your agent harness) to load the company. Implement and test application changes in the **RetroVue** codebase using the workflow and domain boundaries in `COMPANY.md`.

Workflow ideas trace to [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios); **company definition, stack, and roles** are **RetroStudio / RetroVue–specific**. `COMPANY.md` follows the [Agent Companies](https://agentcompanies.io) schema (`agentcompanies/v1`).

## What RetroStudio optimizes for

- **Scheduling** — Channel timeline, **ScheduleService**, EPG horizon: *what should air*.
- **Playout** — **Playlog**, **ChannelManager** / **ProgramDirector**, ffmpeg, overlays: *how it airs*.
- **Ingest** — Media prep, metadata, availability signals: *what is actually airable*.
- **Systems** — **MasterClock** discipline, FastAPI boundaries, cross-domain persistence, documentation coherence.
- **QA** — **Contracts → Invariants → Tests → Code**; integration and broadcast simulation.

Agents are **not** modeled as **live operators** of production RetroVue; they shape what gets built and how it is specified. **Board / owner** retain final authority; agent pushback is **advisory** and evidence-based (`COMPANY.md`).

## Repository layout

| Path | Purpose |
|------|---------|
| [`COMPANY.md`](COMPANY.md) | Mission, architecture alignment, domain boundaries, governance, mandatory engineering order |
| `agents/<role>/AGENTS.md` | Role persona, `reportsTo`, optional skills, responsibilities, anti-overlap rules |
| `teams/<team>/TEAM.md` | Curated groups (`leadership`, `scheduling`, `playout`, `ingest`, `systems`, `qa`) |
| `skills/<skill>/SKILL.md` | Repeatable workflows (some entries are stubs or legacy; use what fits your process) |

## Engineering rules (summary)

Material work follows **Question → Options → Decision → Draft → Approval**. Implementation follows **Contracts → Invariants → Tests → Code** in that order—no implementation-first drops, no skipping tests to merge (`COMPANY.md`).

## Getting started (Paperclip)

Steps follow common Paperclip CLI patterns; confirm current syntax in [Paperclip docs](https://docs.paperclip.ing/start/quickstart) if commands change.

### Prerequisites

- **Node.js** 20+ and **Git**
- Access to your **LLM / Paperclip** setup as required by your workspace
- A local clone of **this** repo (**retro-studio**) and a clone of [**RetroVue**](https://github.com/slbailey/retrovue) (e.g. sibling directories such as `/mnt/retro-studio` and `/mnt/retrovue`)

### Import this company

From a local clone of **retro-studio**:

```bash
npx paperclipai onboard --yes
npx paperclipai company import "/absolute/path/to/retro-studio"
```

Or from your Git remote:

```bash
npx paperclipai company import https://github.com/YOUR_ORG/retro-studio.git
```

The importer reads `COMPANY.md`, `agents/`, `teams/`, and `skills/`. Open the **RetroVue** checkout for service and runtime code:

```bash
git clone https://github.com/slbailey/retrovue.git
```

### Working

- Start from **`COMPANY.md`** and the relevant **director** or **lead** in `agents/`.
- Use **`ceo`** only for cross-domain escalations; do not bypass **directors** or **leads** for ordinary work.
- Keep **clock**, **data ownership**, and **domain** explicit in change descriptions and reviews.

## What’s inside

| Content | Count (approx.) |
|---------|-----------------|
| Agents | 25 |
| Teams | 6 |
| Skills | 37 |

### Agents (summary)

Directory name is `agents/<slug>/`. **Reports to** uses the manager’s slug, or **—** for the root role.

| Slug | Title | Reports to | Function |
|------|-------|------------|----------|
| `ceo` | Studio Head & CEO | — | Cross-domain alignment, escalations from QA/systems; does not replace Board/owner. |
| `scheduling-director` | Scheduling Director | `ceo` | Schedule domain: timeline, ScheduleService, EPG horizon; not Playlog or runtime. |
| `schedule-engineer` | Schedule Engineer | `scheduling-director` | Implements channel timeline + ScheduleService / EPG horizon as one surface. |
| `schedule-constraints-analyst` | Schedule Constraints Analyst | `scheduling-director` | Conflict detection, hard starts, back-to-back rules; reconciliation *inputs*, not Playlog. |
| `playout-director` | Playout Director | `ceo` | Playlog, channel orchestration, ffmpeg Producers, OverlayStages; how authorized intent airs. |
| `playout-lead` | Playout Lead | `playout-director` | Day-to-day playout coordination across playlog, runtime, ffmpeg, overlay engineers. |
| `playlog-engineer` | Playlog Engineer | `playout-lead` | Playlog structure: segments, ordering, durations, transitions, executable constraints. |
| `channel-runtime-engineer` | Channel Runtime Engineer | `playout-lead` | ChannelManager / ProgramDirector: now/next, handoffs, fault posture under MasterClock. |
| `ffmpeg-engineer` | FFmpeg Engineer | `playout-lead` | ffmpeg Producer pipelines: transcode, concat, branding, encoder-chain outputs. |
| `overlay-engineer` | Overlay Engineer | `playout-lead` | OverlayStages: bugs, crawls, lower-thirds; clock-aligned, not a parallel scheduler. |
| `ingest-director` | Ingest Director | `ceo` | Ingest domain: intake, normalization, metadata, availability signals for downstream. |
| `media-prep-engineer` | Media Prep Engineer | `ingest-director` | Media intake and normalization; mezzanine/prep matching Producer expectations. |
| `metadata-engineer` | Metadata Engineer | `ingest-director` | Catalog IDs and descriptive metadata for scheduling / EPG consumers. |
| `availability-analyst` | Availability Analyst | `ingest-director` | Readiness, holds, embargoes; signals so schedule/playout do not assume false airability. |
| `systems-architect` | Systems Architect | `ceo` | Cross-cutting invariants, clock discipline, boundaries; may challenge any domain. |
| `systems-lead` | Systems Lead | `systems-architect` | Coordinates clock, API boundary, persistence, and documentation-architect work. |
| `master-clock-engineer` | Master Clock Engineer | `systems-lead` | MasterClock semantics; sole time authority; no ad hoc wall-clock scattering. |
| `service-boundary-engineer` | Service Boundary Engineer | `systems-lead` | FastAPI / service contracts; preserve domain ownership on integration surfaces. |
| `persistence-governance-engineer` | Persistence Governance Engineer | `systems-lead` | Cross-domain Postgres/SQLAlchemy migrations and shared-table governance. |
| `documentation-architect` | Documentation Architect | `systems-lead` | System-wide doc coherence vs contracts/invariants; contradictions; no implementation code. |
| `qa-director` | QA Director | `ceo` | Contract→test policy, merge-bar advisories; evidence-based; escalates to CEO/Board context. |
| `qa-lead` | QA Lead | `qa-director` | Assigns test, integration QA, and simulation engineers; triage and consolidation. |
| `test-engineer` | Test Engineer | `qa-lead` | Executable tests mapped to contracts and invariants before/around implementation. |
| `integration-qa-engineer` | Integration QA Engineer | `qa-lead` | End-to-end paths: schedule/EPG → Playlog → channel runtime under clock policies. |
| `broadcast-simulation-engineer` | Broadcast Simulation Engineer | `qa-lead` | Scenario and fault simulation for air chains, rolls, overlays, degraded modes. |

*(Delegation, **What You Must NOT Do**, and optional `skills` are defined in each `agents/<slug>/AGENTS.md`.)*

### Teams

| Team slug | Focus |
|-----------|--------|
| `leadership` | CEO + five directors |
| `scheduling` | Timeline, EPG horizon, schedule constraints |
| `playout` | Playlog, channel runtime, ffmpeg, overlays |
| `ingest` | Media prep, metadata, availability |
| `systems` | MasterClock, API boundaries, persistence governance, documentation architect |
| `qa` | Contract tests, integration QA, broadcast simulation |

### Skills

Skills under `skills/` are optional attachments for agents (see YAML in each `AGENTS.md`). Several files are minimal stubs or carry metadata from an earlier studio template; prefer **`COMPANY.md`** methodology and role boundaries when a skill does not apply.

## License

MIT — see [LICENSE](LICENSE).
