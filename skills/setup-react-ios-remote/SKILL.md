---
name: setup-react-ios-remote
description: Bootstrap Gratifire — React iOS app repo, toolchain expectations, and SSH-based development on a remote Mac mini
metadata:
  sources:
    - kind: local
      attribution: Gratifire
      license: MIT
      usage: maintained-in-repo
---

# setup-react-ios-remote

Use this skill when starting or re-onboarding the **Gratifire** iOS (React) project and the **remote Mac mini** build environment.

**Repositories:** Application code lives in **[github.com/slbailey/gratifire](https://github.com/slbailey/gratifire)**. This Agent Company (agents, skills, Paperclip) lives in **[github.com/slbailey/gratifire-game-studios](https://github.com/slbailey/gratifire-game-studios)** — do not confuse the two. The Mac mini checks out the **game** repo; Paperclip imports the **studio** repo.

## Outcomes

- Agreed stack (e.g. **Expo** managed/prebuild, or **React Native CLI**) and how it maps to an **Xcode** workspace on the mini.
- Documented **SSH** access pattern: host, user, project path on the mini, and how code arrives there (git remote, bare pull, or rsync).
- One **golden path** script or checklist: install deps, iOS pods if needed, run Metro (if applicable), build with `xcodebuild` or Xcode scheme, open Simulator.

## Standard questions (answer with the user before changing files)

1. **Framework**: Expo (recommended for faster iteration) or bare React Native?
2. **Repo layout**: monorepo root, `apps/mobile`, or single app folder?
3. **Mac mini**: hostname/IP, SSH user, full path to the checkout (e.g. `~/src/gratifire`).
4. **Signing**: Apple Developer team, bundle ID, provisioning (manual vs automatic), and where certificates live (Keychain on mini only).
5. **Node**: version pinned via `.nvmrc` / `fnm` / `asdf` on **both** dev machine and mini.

## SSH development pattern

Document for the team:

```bash
# Example — adjust user, host, and path
ssh user@gratifire-mac.local
cd ~/src/gratifire
git pull
# Install JS deps on mini when native or lockfile changes
npm ci   # or pnpm install / yarn install
# iOS native deps (React Native / prebuild)
cd ios && pod install && cd ..
# Build (example)
xcodebuild -scheme Gratifire -configuration Debug -sdk iphonesimulator -destination 'platform=iOS Simulator,name=iPhone 16'
```

Rules for agents:

- Prefer **non-interactive** flags; use CI-friendly environment variables for signing when possible.
- Never commit **secrets**, p12 files, or App Store Connect passwords; use Keychain on the mini and CI secret stores.
- If a command must run only on macOS, **state explicitly** that it runs via SSH on the Mac mini.

## Deliverables checklist

- [ ] In the **game** repo (`slbailey/gratifire`): `README` or `docs/DEV_MAC_MINI.md` with SSH host, paths, and copy-paste commands
- [ ] Node version file and package manager lockfile committed
- [ ] iOS bundle identifier and scheme name recorded
- [ ] First successful **Simulator** build from a clean clone on the mini

## Coordination

- **ios-build-engineer**: owns Xcode, CocoaPods, signing, and Simulator/device runs on the mini.
- **react-specialist**: owns app structure, React patterns, and JS tooling.
- **devops-engineer**: optional CI that SSHs or uses a macOS runner to repeat the same steps.
