---
name: Playout
description: Playlog, channel runtime, ffmpeg Producers, and OverlayStages for RetroVue linear execution
slug: playout
manager: ../../agents/playout-director/AGENTS.md
includes:
  - ../../agents/playout-director/AGENTS.md
  - ../../agents/playout-lead/AGENTS.md
  - ../../agents/playlog-engineer/AGENTS.md
  - ../../agents/channel-runtime-engineer/AGENTS.md
  - ../../agents/ffmpeg-engineer/AGENTS.md
  - ../../agents/overlay-engineer/AGENTS.md
  - ../../skills/code-review/SKILL.md
  - ../../skills/architecture-decision/SKILL.md
tags:
  - playout
  - ffmpeg
  - retrovue
---

Playout defines **how** authorized schedule intent becomes on-air execution: **playout-lead** coordinates **playlog-engineer**, **channel-runtime-engineer**, **ffmpeg-engineer**, and **overlay-engineer** under **playout-director**.
