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

### Org overview (reporting spine)

| Tier | Roles |
|------|--------|
| Executive | **ceo** |
| Directors | **scheduling-director**, **playout-director**, **ingest-director**, **systems-architect**, **qa-director** |
| Leads | **playout-lead**, **systems-lead** (incl. **documentation-architect**), **qa-lead** |
| Engineering / analysis | Schedule, playout, ingest, systems, and QA engineers and analysts under the above |

Full reporting lines, delegation, and **What You Must NOT Do** boundaries are in each `agents/*/AGENTS.md`.

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
