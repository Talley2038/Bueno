# HANDOFF.md

Status: Phase 0, repo just scaffolded. Nothing built yet.

## What exists
- docs/PROJECT_RULES.md — governing rules for this project
- docs/ROADMAP.md — phase plan
- This file, DECISIONS.md, ARCHITECTURE.md, PATCH_NOTES.md — stubs

## What's next
Phase 1: bring up Ollama on the Windows desktop, confirm it's reachable
from the Mac over LAN, pick and pull the first model (leaning
Qwen2.5-Coder 14B + Qwen2.5 14B as a starting pair per ROADMAP.md §2
hardware constraints).

## Open questions for owner
- LAN setup between Mac and Windows box — static IP / hostname for the
  Windows machine, or plan to use Tailscale?
- Confirm Windows box stays on/reachable during work sessions, or needs
  wake-on-LAN handling?

## Known blockers
None yet.
