# Gratifire Game Studios

> **This repository** ([**slbailey/gratifire-game-studios**](https://github.com/slbailey/gratifire-game-studios)) is the **Agent Company** for **Gratifire**: **37 coordinated AI agents** for creative direction, engineering, design, art, audio, narrative, QA, and production. The **actual iOS game** is built with **React** in a **separate repo**: [**slbailey/gratifire**](https://github.com/slbailey/gratifire). **Xcode builds and native iOS work run on a remote Mac mini via SSH** against the **game** checkout.

| | Repository | Purpose |
|---|-------------|---------|
| **Game** | [github.com/slbailey/gratifire](https://github.com/slbailey/gratifire) | React iOS app source, tests, app CI, `docs/DEV_MAC_MINI.md` |
| **Studio (this repo)** | [github.com/slbailey/gratifire-game-studios](https://github.com/slbailey/gratifire-game-studios) | `COMPANY.md`, `agents/`, `teams/`, `skills/`, Paperclip — import **this** into Paperclip |

Workflow patterns derive from [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios); roles, stack, and **two-repo layout** are **Gratifire-specific**. This package follows the [Agent Companies](https://agentcompanies.io) schema (`COMPANY.md`).

## Layout of **this** repo (studios)

| Path | Purpose |
|------|---------|
| `COMPANY.md` | Company metadata, goals, architecture (React iOS + Mac mini + repo split) |
| `agents/<role>/AGENTS.md` | Persona, reporting line, skills, boundaries |
| `teams/<team>/TEAM.md` | Curated groups (e.g. `react-ios`, `engineering`, `creative`) |
| `skills/<skill>/SKILL.md` | Repeatable workflows (sprints, GDD, release, **setup-react-ios-remote**, …) |
| `projects/gratifire-kickoff/` | Sample project + tasks for early-phase work |
| `.paperclip.yaml` | [Paperclip](https://paperclip.ing) adapter hints (models, optional secrets) |

## Getting started with Paperclip (step by step)

These steps match the current Paperclip CLI patterns. If a command fails, check the [Paperclip documentation](https://docs.paperclip.ing/start/quickstart) for the latest syntax — the product evolves quickly.

### 1. Prerequisites

- **Node.js** 20 or newer installed.
- **Git** and a terminal (PowerShell on Windows is fine).
- **Anthropic / Claude** access configured the way Paperclip expects (see Paperclip onboarding output).
- A **Mac mini** (or other Mac) with **Xcode**, reachable by **SSH**, for iOS builds — optional at import time, required before you ship native builds.

### 2. Install and onboard Paperclip

Run Paperclip’s onboarding so the control plane and local tooling are ready:

```bash
npx paperclipai onboard --yes
```

Complete any prompts to sign in, pick a workspace, or install dependencies. When onboarding finishes, note where Paperclip expects **companies** and **projects** to live.

### 3. Import this company (studios repo only)

Import **[slbailey/gratifire-game-studios](https://github.com/slbailey/gratifire-game-studios)** — not the game repo. From a local clone:

```bash
npx paperclipai company import "/absolute/path/to/gratifire-game-studios"
```

Or from GitHub:

```bash
npx paperclipai company import https://github.com/slbailey/gratifire-game-studios.git
```

The importer reads `COMPANY.md`, `agents/`, `teams/`, and `skills/`. It does **not** contain the React app; clone [**slbailey/gratifire**](https://github.com/slbailey/gratifire) separately for coding the game.

### 4. Wire optional secrets (GitHub, stores)

If Paperclip supports environment secrets for agents, set them where the CLI or UI indicates. This repo’s `.paperclip.yaml` marks **`GH_TOKEN`** as optional for **devops-engineer** and **release-manager** when you automate PRs or releases.

### 5. Configure the Mac mini (engineering)

Before agents run real iOS commands:

1. Enable **SSH** on the Mac (`System Settings` → `General` → `Sharing` → **Remote Login**).
2. From your dev machine, verify: `ssh youruser@your-mac-hostname`.
3. Clone **[github.com/slbailey/gratifire](https://github.com/slbailey/gratifire)** onto the Mac at a stable path (e.g. `~/src/gratifire`).
4. In the **game** repo, add `docs/DEV_MAC_MINI.md` (or equivalent) with host, user, paths — the **setup-react-ios-remote** skill describes the checklist.

Agents are instructed to treat **SSH on the Mac mini** as the default place for **`xcodebuild`**, **Simulator**, **pods**, and **signing**.

### 6. Start working

- Open the imported **Gratifire** company in the Paperclip UI (if your install provides one) or use the CLI commands shown after `onboard`.
- Begin with **`start`** or **`setup-react-ios-remote`** (see `skills/`) and the **producer** / **technical-director** / **ios-build-engineer** as appropriate.
- Follow the studio protocol in `COMPANY.md`: **Question → Options → Decision → Draft → Approval** before large or irreversible changes.

### 7. Optional: local folder name

If your clone still lives under a legacy folder name (e.g. `donchitos-game-studio`), rename it to `gratifire-game-studios` to match the GitHub repo and update your Paperclip import path in step 3.

### 8. Link the two repos

In **gratifire**’s README, link to **gratifire-game-studios** for “how we run the AI studio.” In **gratifire-game-studios**’s README (this file), you already link to **gratifire** for the app.

---

## What’s inside

| Content | Count |
|---------|-------|
| Agents | 37 |
| Skills | 37 |

### Agents (summary)

| Agent | Role | Reports to |
|-------|------|------------|
| CEO | Studio head | — |
| Creative Director | Creative vision | ceo |
| Technical Director | Architecture, React iOS stack, Mac mini pipeline | ceo |
| Producer | Schedule, coordination | ceo |
| Lead Programmer | Engineering lead | technical-director |
| React Specialist | React / TypeScript architecture | lead-programmer |
| iOS Build Engineer | Xcode, signing, SSH Mac mini builds | lead-programmer |
| Gameplay Programmer | Mechanics in client code | lead-programmer |
| Platform & Runtime Programmer (`engine-programmer`) | Metro, bridges, runtime | lead-programmer |
| UI Programmer | React screens | lead-programmer |
| AI Programmer | In-game AI / helpers | lead-programmer |
| Network Programmer | APIs, realtime, sync | lead-programmer |
| Tools Programmer | CLIs, pipelines, dev tools | lead-programmer |
| QA Lead | Test strategy | technical-director |
| QA Tester | Execution | qa-lead |
| Performance Analyst | Mobile / JS performance | technical-director |
| Game Designer | Core design | creative-director |
| Systems Designer | Systems | game-designer |
| Level Designer | Levels / content pacing | game-designer |
| Economy Designer | Economy | game-designer |
| Art Director | Visual direction | creative-director |
| Technical Artist | 2D / mobile art pipeline | art-director |
| UX Designer | UX flows | art-director |
| Audio Director | Audio vision | creative-director |
| Sound Designer | Sound | audio-director |
| Narrative Director | Story | creative-director |
| Writer | Text | narrative-director |
| World Builder | Lore | narrative-director |
| Accessibility Specialist | A11y | producer |
| Analytics Engineer | Telemetry | producer |
| Community Manager | Community | producer |
| DevOps Engineer | CI, SSH automation | producer |
| Localization Lead | i18n | producer |
| Live Ops Designer | Live ops | producer |
| Prototyper | Rapid prototypes | producer |
| Release Manager | TestFlight / App Store | producer |
| Security Engineer | Security | producer |

*(Full detail and skills are in each `agents/*/AGENTS.md`.)*

### Skills (in-repo)

Skills live under `skills/*/SKILL.md`. Notable for this stack:

| Skill | Description |
|-------|-------------|
| **setup-react-ios-remote** | React iOS repo + **SSH Mac mini** golden path |
| design-system | GDD authoring |
| sprint-plan, milestone-review, gate-check | Production rhythm |
| team-ui, team-audio, team-narrative, … | Cross-discipline orchestration |
| launch-checklist, release-checklist, patch-notes | Shipping |

Skill metadata uses **`repo: slbailey/gratifire-game-studios`** with paths under `skills/…` in **this** repo. Original workflow ideas trace to [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios).

---

## License

MIT — see [LICENSE](LICENSE).
