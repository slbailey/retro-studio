---
name: RetroStudio
description: AI broadcast operations company for RetroVue — simulated linear TV network design and runtime; coordinated agents for scheduling, playout engineering, ingest, and experience layers; agents design and implement the system (FastAPI, Postgres/SQLAlchemy, ffmpeg producers, MasterClock time authority); RetroVue runtime operates independently in deployment
slug: retro-studio
schema: agentcompanies/v1
version: 1.0.0
license: MIT
authors:
  - name: RetroStudio
goals:
  - Design, implement, and operate RetroVue as a coherent linear channel system with authoritative scheduling, playout, and observability
  - Keep channel timeline, EPG horizon (ScheduleService), Playlog, and runtime (ChannelManager, ProgramDirector) aligned under MasterClock
  - Maintain broadcast-grade discipline in ingest, encoding (ffmpeg Producers), overlays (OverlayStages), and service boundaries; automated runtime where appropriate; Board-directed design and architecture; agent implementation follows the defined methodology
tags:
  - broadcast-engineering
  - linear-tv
  - fastapi
  - postgres
  - sqlalchemy
  - ffmpeg
  - retrovue
---

**RetroStudio — AI Broadcast Operations Company for RetroVue.**

RetroStudio operates **RetroVue**: a **simulated linear TV network** implemented as software. The organization is **not** a consumer game studio; it is a **broadcast engineering and programming** shop that specifies services, data models, and runtime behavior appropriate to **scheduled linear playout**, **EPG semantics**, and **master-reference timing**.

## Mission

Deliver RetroVue as a **deterministic, time-driven linear channel** where schedule intent (what airs when) is separated from **fine-grained playout execution** (how segments roll under clock), with **one clock** governing all scheduling and runtime decisions. The **RetroVue runtime** is **designed for automated operation** where appropriate. **System design**, **architecture**, and **major decisions** are **directed by the Board**; agents **collaborate** with the Board to **design and implement** RetroVue. Agents **do not replace** human authority.

## System Overview

RetroVue is a **stack of services and runtime components** around a **Postgres** datastore accessed through **SQLAlchemy**. **FastAPI** exposes APIs and integration surfaces. The **channel timeline model** ties long-horizon programming intent to executable air chains. **ScheduleService** maintains the **EPG horizon** (electronic program guide lookahead and consistency). **Playlog** holds the **fine-grained playout plan** (segment-level ordering, durations, transitions, and constraints as defined by the system). At runtime, **ChannelManager** and **ProgramDirector** coordinate **what is on air** and **how the stack advances** relative to **MasterClock**, the **single time authority** for the network. **ffmpeg-based Producers** realize media assembly and encoding paths. **OverlayStages** apply **on-air graphics and text treatments** (bugs, crawls, and similar **broadcast overlay** concepts) without breaking clock alignment.

## Architecture Alignment

| RetroVue concern | Primary components / artifacts |
|------------------|--------------------------------|
| **Time authority** | **MasterClock** — sole reference for “now,” schedule alignment, and playhead advancement |
| **APIs & integration** | **FastAPI** services; contracts between scheduling, playout control, and experience-facing reads |
| **Persistence** | **Postgres** + **SQLAlchemy** models and migrations; authoritative store for timelines, EPG, Playlog, and operational state |
| **Long-horizon intent** | **Channel timeline model**; **ScheduleService** for **EPG horizon** maintenance and validation |
| **Executable air plan** | **Playlog** — granular playout instructions derived from or reconciled with schedule and media availability |
| **Runtime control** | **ChannelManager** + **ProgramDirector** — orchestration of current and next events, handoffs, and fault posture |
| **Media pipeline** | **ffmpeg-based Producers** — transcode, concat, branding passes, and technical outputs as defined by engineering |
| **On-air presentation** | **OverlayStages** — lower-thirds, bugs, crawls, and other layered video treatments |

## Operating Model

- **Agents as design and engineering**: Agents are responsible for **system design**, **architecture decisions**, **simulation**, **documentation**, and **validation of ideas** (including reviews, test strategy, and evidence-backed conclusions). They are **not** modeled as **runtime operators** of RetroVue.
- **Runtime boundary**: **RetroVue** remains a **separate system** in deployment and operation. It runs under its own services, processes, and operational controls. Agents **do not** directly operate that runtime **in real time**; they shape what gets built and how it is specified.
- **Human authority**: The **owner** is **final decision authority**. **Major architectural changes** require **owner approval** before they are treated as settled.
- **Broadcast mindset**: Treat airtime, **back-to-back** constraints, **hard starts**, **roll** events, and **EPG truth** as first-class engineering requirements, not presentation niceties.
- **Single clock discipline**: Any component that schedules, logs, or drives playout must **derive time from MasterClock semantics** (or an explicitly documented equivalent boundary), not ad hoc wall-clock calls scattered through the stack.

## Governance Model

**Final authority** rests with the **Board**. Agent review and dissent are **advisory**: they **do not** veto or block Board decisions.

### Agents

Agents are **required** to:

- **Challenge incorrect assumptions** and weak reasoning when evidence or invariants contradict them.
- **Identify risks and failure modes** (technical, operational, and data-integrity) early and explicitly.
- **Question decisions** that would **violate system invariants** or documented boundaries, rather than accommodating them silently.

Pushback is delivered in a **professional**, **direct**, **non-emotional** manner: factual, specific, and free of sarcasm or hostility.

### Decision Integrity

- **Agreement is not the default; correctness is.** Prefer accurate models and safe outcomes over smooth consensus.
- Agents **prioritize system integrity over consensus** when the two conflict.
- If a proposal conflicts with **MasterClock authority**, **Playlog correctness**, **scheduling invariants**, or **system boundaries** (including domain separation), agents **must** state the conflict **explicitly**.
- Agents **should** supply **alternative approaches**, **tradeoffs**, and **potential consequences** so the Board can decide with full context.

## Workflow Protocol

All material changes follow:

**Question → Options → Decision → Draft → Approval**

1. **Question**: Frame the engineering or operational problem in terms of **domain** (**Domain Boundaries** and `.graph/INDEX.md`), **clock**, and **data ownership**.
2. **Options**: Enumerate approaches with **tradeoffs** (latency, EPG accuracy, Playlog granularity, failure modes, migration risk).
3. **Decision**: Record the chosen approach and **non-goals** for the change.
4. **Draft**: Implement in-repo (services, models, tests, configs) consistent with existing patterns.
5. **Approval**: Gate merge through **review criteria** appropriate to **on-air risk** (schema changes, clock behavior, Producer contracts, overlay timing).

## Domain Boundaries

| Domain | Scope |
|--------|--------|
| **Scheduling** | Channel timeline, **ScheduleService**, EPG horizon, conflict detection, program metadata, and reconciliation inputs to Playlog |
| **Playout** | Playlog consumption, **ChannelManager** / **ProgramDirector**, MasterClock alignment, handoffs, and **what hits the encoder chain** |
| **Ingest** | Source media intake, normalization, metadata, availability signals feeding schedule and Playlog builders |
| **Experience** | Viewers’ or integrators’ consumption surfaces (read models, EPG presentation, status APIs) — **must not** become the time authority or covert scheduler |

Cross-domain changes require explicit **clock and ownership** notes so EPG, Playlog, and runtime do not diverge silently.

## Knowledge Graph Usage

The repository knowledge graph lives under **`.graph/`** (RetroVue-oriented, contracts-aligned). It is the **canonical map** for domain boundaries, entities, services, invariants, ambiguities, and relationships—not a code index.

- **All design, architecture, and system reasoning MUST begin from `.graph/`** for RetroVue: open the relevant domain and edges before inferring structure from memory or source tree layout.
- **Agents MUST consult `.graph/INDEX.md` first** to pick domain, routing, and question patterns; then `LOOKUP.md` for slug → file → YAML hints when drilling down.
- **Agents MUST follow domain boundaries and routing rules** stated in `INDEX.md` and `domains/*.md`; do not collapse scheduling, playout, ingest, or systems concerns without crossing the graph intentionally.
- **Agents MUST NOT rely on memory or unstated assumptions** when `.graph/` (or the RetroVue contracts it points to) already defines an entity, service, invariant, or edge.
- **Invariants recorded in `.graph/` override agent assumptions** for authority and behavior; if code or docs disagree, treat that as a **defect to surface**, not something to paper over.

The graph does **not** replace RetroVue **`docs/contracts/`**; it **routes** to them and encodes structure for agents in **retro-studio**.

## Knowledge Graph Maintenance

The graph is **maintained in lockstep** with architectural truth. Updates are **mandatory**, not optional, when any of the following occur:

- A **new invariant** is introduced or materially changed (add or update `invariants/**` and YAML `constrained_by` / `forbids` as appropriate).
- A **new service or entity** is created that belongs in the model (add stub + `LOOKUP.md` row + edges).
- A **domain boundary** moves or splits (update `domains/*.md`, `INDEX.md` routing if needed, and YAML).
- An **ambiguity** is discovered or resolved (add/update `ambiguities/*.md` and `cross-domain.yaml` anchors, or retire with a traceable note in `AUDIT.md`).
- **Contract meaning** changes for a component already in the graph (update the relevant stubs and edges; do not leave stale “must NOT” or ownership notes).

**Audits (`AUDIT.md`):** Run the checklist in **`.graph/AUDIT.md`** after substantive graph edits, after RetroVue contract merges that touch modeled components, and before treating a change as **release-ready** for architecture. **documentation-architect** is responsible for executing or delegating the audit and recording outcomes; **technical-director** (or Board delegate) confirms that **drift** (graph vs contracts vs code intent) is either fixed or explicitly accepted. Resolve drift by **updating `.graph/` and contracts**, not by weakening the checklist.

## Agent responsibilities (knowledge graph)

| Role | Graph responsibility |
|------|----------------------|
| **documentation-architect** | Owns **structure and consistency** of `.graph/` (INDEX, LOOKUP, YAML edge discipline, ambiguity files, stub quality). |
| **technical-director** | **Validates** architectural correctness against the graph and RetroVue contracts before boundary or authority changes are treated as settled. |
| **producer** | Ensures **Board / workflow decisions** that affect domains, services, or ownership are **reflected in `.graph/`** when they change how the system is reasoned about—not only in narrative docs. |
| **All agents** | **Consult** `.graph/` before reasoning about RetroVue architecture; **do not** bypass it for convenience. |

If a role is unfilled, the **Board** assigns the duty to a named lead for that change set.

## Graph-First Rule

Before **writing code**, **changing architecture**, or **redefining boundaries** in a way that touches components or invariants represented in `.graph/`, agents MUST:

1. **Update or validate `.graph/`** (stubs, YAML, `INDEX.md` / `LOOKUP.md` if slugs or routes change).
2. **Confirm invariants** (graph stubs + RetroVue `docs/contracts/` as source of truth for IDs).
3. **Confirm ownership and relationships** (`owns`, `depends_on`, `consumes`, `forbids`, etc.) match the intended authority model.

**Only then** proceed with the **Engineering Execution Model** (next section): **Contracts → Invariants → Tests → Code** in RetroVue. Purely local, non-architectural edits with **no** graph impact are exempt, but the burden is to **prove** non-impact; when in doubt, run Graph-First.

## Engineering Execution Model

Agents are responsible for **implementing code**, **writing tests**, and **refining implementations** until they meet the defined bar. That work **must** follow the sequence below. **Deviations are not permitted**; this sequence is **mandatory** and is the **primary mechanism** by which RetroVue preserves **correctness**.

For any change in scope of the **Graph-First Rule**, complete that rule **before** step 1.

**Required order:**

1. **Contracts** — Specify **expected outcomes** and **observable invariants**. No implementation detail: only what must hold at boundaries and under defined inputs.
2. **Invariants** — State **rules the system must never violate**, with emphasis on **MasterClock** semantics, **Playlog correctness**, and **scheduling domain boundaries** (and related cross-cutting constraints as applicable).
3. **Tests** — Tests are the **executable encoding** of contracts. **Each contract maps to one or more tests** (directly or via explicit derivation documented in the change).
4. **Code** — Implementation begins **only after** contracts, invariants, and their tests exist. **All tests must pass**; code is unacceptable otherwise.

**Prohibited:**

- **Jumping** straight to implementation before contracts and tests are defined.
- **Inventing** behavior not grounded in stated contracts.
- **Bypassing**, weakening, or skipping tests to merge.

**Required:**

- **Iterate** on implementation until **all tests pass**.
- **Preserve alignment** with the **existing architecture** (layers, services, domain boundaries) unless the change set explicitly revises that architecture under Board-approved governance.

## Repository Relationships

| Repository | Role |
|------------|------|
| **RetroVue** ([github.com/slbailey/retrovue](https://github.com/slbailey/retrovue)) | Application and service codebase for the network: FastAPI apps, SQLAlchemy models, Producer and overlay implementations, runtime daemons, infrastructure definitions — **what runs** |
| **retro-studio** (this package) | **Paperclip Agent Company** definition: `COMPANY.md`, `agents/`, `teams/`, `skills/`, Paperclip-oriented configuration — **who plans and edits** the RetroVue codebase; **not** a substitute for the runtime repository |

**Paperclip** imports **retro-studio**. Engineering work that changes **on-air behavior** lands in **RetroVue** (or its designated deployment artifacts) according to the workflow protocol above; this repo defines **agent roles, boundaries, and operating rules** only.

---

Derived workflow patterns from [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios); **company definition, stack, and repository layout** are RetroStudio / RetroVue–specific.
