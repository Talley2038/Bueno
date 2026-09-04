# DECISIONS

Locked decisions with reasoning. Each entry answers "we decided X because Y."

Only decisions that are done get logged here. Open questions live in `HANDOFF.md`. Scope items live in `ROADMAP.md`.

Format: terse, first letter capitalized, no terminal periods. `Decision:` as standalone label. `Reason:` as second label. Every entry dated.

---

## `2026-09-04`

### Inference server: Ollama on Windows desktop
- **Decision:** Inference runs on the Windows desktop (RTX 5070, 12GB VRAM) via Ollama, not on the Mac
- **Reason:** The 5070 is the only GPU in the household setup. Mac is dev/client only. Ollama exposes an OpenAI-compatible API out of the box, lowest-friction path to a working local inference server

### Chat frontend: Open WebUI
- **Decision:** Open WebUI as the chat interface, connecting to the Ollama endpoint
- **Reason:** Most mature self-hosted ChatGPT-style frontend with native Ollama support, multi-model switching, file upload, and web search hooks. Actively maintained, widely used

### Networking: Tailscale over static LAN IP
- **Decision:** Tailscale mesh connecting Mac, Windows box, and husband's device(s), rather than a static LAN IP or hostname
- **Reason:** Owner works remotely from the inference host (currently away for 7 days, will continue working from cafes). Two-user access from arbitrary locations is the stated goal. Static LAN IP only covers same-network. Exposing the inference server directly to the open internet is outside the privacy boundary (Rule 28). Tailscale handles NAT traversal and encryption without opening ports

### WoL: deferred, not built
- **Decision:** Not building Wake-on-LAN support in P1. Windows box configured to not sleep once set up as inference host
- **Reason:** Stated eventual target is box available ~24/7, which removes the wake problem. Re-examine only when the box is in a testable single-user state and actual usage data shows idle time worth addressing — see R6 backlog

### Repo: private, single repo
- **Decision:** Single private repo at `github.com/Talley2038/Bueno`
- **Reason:** No reason to expose local infra/config publicly. No reason to split — one project, one repo

### Doc structure: R0–R7 roadmap, OPERATIONS_GUIDE as single rule source
- **Decision:** ROADMAP uses R0–R7 section structure with status legend and task-level checklist. OPERATIONS_GUIDE.md is the single canonical rule set, pasted into the Claude Project instructions field. PROJECT_RULES.md retired
- **Reason:** Adopted from a working project with 30+ sessions of proven doc-structure evolution. R0–R7 answers "what's next" at a glance. Single rule file eliminates two-copy drift
