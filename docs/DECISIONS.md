# DECISIONS

Locked decisions. Each entry answers "decided X because Y."

Only closed decisions logged here. Open questions live in `HANDOFF.md`. Scope items live in `ROADMAP.md`.

Format: terse, first letter capitalized, no terminal periods. `Decision:` and `Reason:` as standalone labels. Every entry dated.

---

## `2026-09-04`

### Inference server: Ollama on Windows desktop
- **Decision:** Inference runs on the Windows desktop (RTX 5070, 12GB VRAM) via Ollama, not on the Mac
- **Reason:** The 5070 is the only GPU in the setup. Mac is dev/client only. Ollama exposes an OpenAI-compatible API out of the box, lowest-friction path to a working local inference server

### Chat frontend: Open WebUI
- **Decision:** Open WebUI as the chat interface, connecting to the Ollama endpoint
- **Reason:** Most mature self-hosted ChatGPT-style frontend with native Ollama support, multi-model switching, file upload, and web search hooks. Actively maintained, widely used

### Networking: Tailscale over static LAN IP
- **Decision:** Tailscale mesh connecting all devices, rather than a static LAN IP or hostname
- **Reason:** Primary dev machine is frequently remote (cafes, travel). Two-user access from arbitrary locations is a requirement. Static LAN IP only covers same-network. Exposing the inference server to the open internet violates the privacy boundary (Rule 28). Tailscale handles NAT traversal and encryption without opening ports

### WoL: deferred, not built
- **Decision:** Not building Wake-on-LAN in P1. Windows box configured to not sleep once set up as inference host
- **Reason:** Target state is box available ~24/7, which removes the wake problem. Re-examine only in a testable single-user state when actual usage data shows idle time worth addressing. See R6 backlog

### Repo: private, single repo
- **Decision:** Single private repo at `github.com/Talley2038/Bueno`
- **Reason:** No reason to expose local infra/config publicly. No reason to split: one project, one repo

### Doc structure: R0-R7 roadmap, OPERATIONS_GUIDE as single rule source
- **Decision:** ROADMAP uses R0-R7 section structure with status legend and task-level checklist. OPERATIONS_GUIDE.md is the single canonical rule set, pasted into the Claude Project instructions field. PROJECT_RULES.md retired
- **Reason:** Adopted from a working project with proven doc-structure evolution. R0-R7 answers "what's next" at a glance. Single rule file eliminates two-copy drift

## `2026-09-04` (rule amendment, Rule 33)

### New Rule 36: ASCII-only characters
- **What:** All docs and code comments restricted to standard US keyboard characters. No em dash, en dash, middle dot, ellipsis character, section sign, or unicode math symbols
- **Why:** Manual cleanup was needed across every doc to remove em dashes, middle dots, ellipsis characters, and the section sign after the fact. Codifying this prevents the same cleanup pass on every future doc edit

### New Rule 37: First-party document voice
- **What:** Docs (outside ARCHITECTURE.md and OPERATIONS_GUIDE.md) read as if written directly, not as an external description. No third-person framing of the person doing the work. Other people mentioned are described generically unless naming them is functionally necessary
- **Why:** Original docs read as machine-generated, with third-person references and unnecessary personal detail. Required a manual voice pass to fix

### New Rule 38: Roadmap task granularity
- **What:** Every roadmap task requires a testable done-state. Every phase requires a closing gate. Tasks not blocked by the phase's stated blocker get pulled into the active phase rather than bundled with blocked work
- **Why:** Original ROADMAP had vague task descriptions and lumped all P1 work as blocked, hiding several tasks that were actually doable immediately. Required a manual rewrite to fix
