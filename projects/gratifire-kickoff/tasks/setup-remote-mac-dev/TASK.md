---
name: Remote Mac mini & React iOS setup
assignee: ios-build-engineer
project: gratifire-kickoff
---

Establish **SSH** access to the **Mac mini**, document the checkout path, and produce a **golden-path** for installing dependencies, running **pods** if needed, and producing a **Simulator** build for Gratifire. The checkout on the mini must be **[github.com/slbailey/gratifire](https://github.com/slbailey/gratifire)** (the game repo), not the studios repo. Confirm **Node** and **Xcode** versions, **bundle ID**, and signing approach with the user. Apply the **setup-react-ios-remote** skill.

## Deliverables

- In **slbailey/gratifire**: `docs/DEV_MAC_MINI.md` (or equivalent) with host, user, paths, and copy-paste commands
- Successful **Simulator** build from a clean pull on the mini
- Notes for **devops-engineer** if CI should mirror the same steps
