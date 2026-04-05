---
name: Gratifire
description: Game design studio building the Gratifire iOS game with React — coordinated AI agents for creative, engineering, QA, and production, with development executed over SSH on a remote Mac mini
slug: gratifire
schema: agentcompanies/v1
version: 1.0.0
license: MIT
authors:
  - name: Gratifire
goals:
  - Ship Gratifire as a polished iOS application built primarily with React (e.g. React Native / Expo)
  - Keep creative and production workflows aligned while engineering runs builds, tests, and Xcode work on a remote Mac mini via SSH
  - Maintain quality through reviews, playtesting, and release gates appropriate for the App Store
tags:
  - game-development
  - ios
  - react
  - react-native
  - mobile
  - remote-build
---

Gratifire is a **game design studio** focused on one product: **Gratifire**, an iOS game delivered as a **React-based** app. The org mirrors a small professional studio (creative, engineering, narrative, audio, QA, production) while the **technical stack is fixed**: JavaScript/TypeScript and React patterns on the client, native iOS packaging and signing through Apple’s toolchain, executed on a **remote Mac mini** when local development machines are not macOS.

## Two repositories

| Repository | GitHub | Contents |
|------------|--------|----------|
| **Game (application)** | [github.com/slbailey/gratifire](https://github.com/slbailey/gratifire) | React iOS app source, `package.json`, `ios/`, tests, app CI, `docs/DEV_MAC_MINI.md`, everything that ships to players |
| **Studio (Agent Company)** | [github.com/slbailey/gratifire-game-studios](https://github.com/slbailey/gratifire-game-studios) | This package: `COMPANY.md`, `agents/`, `teams/`, `skills/`, Paperclip config — **no** substitute for the game codebase |

**Paperclip** imports the **studio** repo. The **Mac mini** clones or pulls the **game** repo. Cross-link both READMEs so contributors know where to work.

## Architecture

| Layer | Responsibility |
|-------|----------------|
| **Game & UX** | Creative direction, game design, narrative, audio, art, UX — same studio disciplines, scoped to a mobile React experience |
| **Application code** | React components, state, gameplay logic, networking — owned by **lead-programmer** with **react-specialist** and **gameplay-programmer** |
| **Platform / iOS** | Xcode projects, schemes, signing, TestFlight, App Store Connect, Simulator/Device runs — owned by **ios-build-engineer** (typically via SSH to the Mac mini) |
| **Infra** | CI, secrets, SSH access, automation hooks — **devops-engineer** with **ios-build-engineer** |

## Remote Mac mini workflow

Engineering agents assume **authoritative iOS builds and Xcode operations happen on a Mac mini** reached with **SSH** (e.g. `ssh user@gratifire-mac.local`). Day-to-day flow:

1. Edit and review TypeScript/React in the **game** repo ([slbailey/gratifire](https://github.com/slbailey/gratifire)) on any OS.
2. Sync or push changes so the Mac mini has the **game** repo’s current tree (git pull, rsync, or CI artifact — as the team defines).
3. Run installs, `pod install` if applicable, `xcodebuild`, tests, and Simulator/Device deploys **over SSH** on the mini.
4. Capture logs and artifacts back to the developer (scp, CI upload, or shared folder).

Agents document exact commands in runbooks; they never invent credentials or bypass signing rules.

## Operating model

- **Pipeline**: Same phase mindset as before (ideation → post-launch), tuned for a single React iOS product.
- **Hub-and-spoke**: Producer coordinates; **technical-director** owns stack and architecture; **creative-director** owns player-facing vision.
- **Collaboration protocol**: **Question → Options → Decision → Draft → Approval** before material file changes.

Derived workflow patterns from [Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios); stack, **two-repo layout**, and company definition are Gratifire-specific.
