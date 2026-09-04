# DECISIONS.md

## 2026: Initial architecture
Decision: Ollama as inference server, Open WebUI as chat frontend.
Reason: Lowest-friction path to a working local LLM with an
OpenAI-compatible API; both are actively maintained and widely used.

Decision: Inference runs on the Windows desktop (RTX 5070), not the Mac.
Reason: The 5070's 12GB VRAM is the only GPU in the household setup;
Mac is dev-only for now.

Decision: Repo is private.
Reason: No reason to make local infra/config public by default.

## Networking: Tailscale over static LAN IP
Decision: Use Tailscale to connect Mac, Windows inference host, and
husband's device(s) into one private mesh network, rather than a static
LAN IP/hostname.
Reason: Owner is currently working remote (no home LAN access for 7 days),
will continue working from cafes/etc. ongoing, and the stated goal is
two-user access from anywhere. Static LAN IP only solves same-network
access; Tailscale solves the actual requirement without exposing the
inference server to the open internet. Setup deferred until owner is
physically back at the Windows box (see ROADMAP.md §7).

## Wake-on-LAN: deferred, not built now
Decision: Not building WoL support in Phase 1. Windows box configured to
not sleep once set up as inference host.
Reason: Stated eventual target is the box available ~24/7, which removes
the "wake a sleeping/off box remotely" problem WoL solves. Revisit only if
usage pattern (single-user, testable state) shows the box is idle enough
that always-on has a meaningful power cost — see ROADMAP.md §6 backlog
item.
