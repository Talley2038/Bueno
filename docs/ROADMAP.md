# ROADMAP

Canonical scope + phase map + task-level status. Read R1–R3 at the start of every session; read R0 always.

**Status legend:** `[ ]` open · `[~]` in progress · `[x]` done · `[!]` blocked
**Format:** `- [x] ID · Name · started YYYY-MM-DD · done YYYY-MM-DD · vX.Y.Z`. Version tag only when the item lands with a bump.

---

## R0. At-a-glance

- **Phase:** **P0 OPEN** (scaffolding)
- **Version:** `v0.1.0` (initial scaffold)
- **Repo:** https://github.com/Talley2038/Bueno (private)
- **Current milestone:** P0: repo structure, docs, no code yet. P1 blocked on regaining physical to desktop (~7 days from 2026-09-04)
- **Active blockers:** No physical access to Windows desktop until ~2026-09-11
- **Last audit:** None yet (first phase)

---

## R1. North Star

Build and maintain Bueno (a private, locally-run LLM assistant that runs entirely on the owner's own hardware). Windows desktop hosts inference via Ollama; Mac is the occasional dev/client machine. Accessible from anywhere via Tailscale. Two planned users.

Capabilities: coding help, recipe generation, web-search-augmented answers, Excel/data automation, general assistant work. No cloud dependency for inference. No data leaves the LAN except explicit tool calls (web search API).

---

## R2. Locked Architecture

Non-negotiable unless explicitly reopened in `DECISIONS.md`.

- **Inference server:** Ollama on the Windows desktop (RTX 5070, 12GB VRAM)
- **Model class:** 7B–32B open-weight, 4-bit quantized. Model + quantization pinned explicitly (Rule 25)
- **Chat frontend:** Open WebUI connected to Ollama endpoint over Tailscale
- **Network:** Tailscale mesh — Mac, Windows box, husband's device(s)
- **Privacy boundary:** nothing leaves the machine except explicit, owner-approved tool calls (Rule 28)
- **Repo:** single private repo, `github.com/Talley2038/Bueno`

---

## R3. Constraints

1. Inference host GPU: RTX 5070, 12GB VRAM — caps model size at ~14B fully on-GPU or ~32B with CPU offload
2. Dev machine: Mac (current primary). Inference host: Windows desktop
3. Owner works remotely from the inference host — Tailscale is mandatory, not optional
4. Two users eventually (owner + husband), both from arbitrary locations
5. No cloud inference dependency. Local model only
6. Windows box intended to run ~24/7 once operational

---

## R4. Current Phase — P0 Scaffolding

- [x] T0.1 · Repo created and initial scaffold pushed · 2026-09-04
- [x] T0.2 · Networking decision locked (Tailscale) · 2026-09-04
- [x] T0.3 · WoL deferred to backlog with re-examine trigger · 2026-09-04
- [x] T0.4 · Docs restructured to R0–R7, OPERATIONS_GUIDE, GLOSSARY · 2026-09-04

**P0 gate:** all docs in place, decisions locked, ready to begin P1 when physical access to Windows box is available.

### P1 — Inference Host Bring-up

- [ ] T1.1 · Install Ollama on Windows box
- [ ] T1.2 · Install Tailscale on Windows box and Mac, confirm mesh connectivity
- [ ] T1.3 · Pull first model pair (Qwen2.5-Coder 14B + Qwen2.5 14B), confirm inference works locally on the box
- [ ] T1.4 · Confirm Ollama API reachable from Mac over Tailscale
- [ ] T1.5 · Pin model + quantization in config, log in DECISIONS.md

### P2 — Chat Interface

- [ ] T2.1 · Install Open WebUI, connect to Ollama endpoint
- [ ] T2.2 · Confirm multi-model switching works (coder vs. generalist)
- [ ] T2.3 · Confirm husband's device can reach Open WebUI via Tailscale

### P3 — Web Search Tool

- [ ] T3.1 · Decide search backend (SearXNG self-hosted vs. Brave Search API), log in DECISIONS.md
- [ ] T3.2 · Wire search into Open WebUI
- [ ] T3.3 · Test: model can search and cite results in a response

### P4 — Excel / Code Execution Tool

- [ ] T4.1 · Build Python sandbox callable as a tool (openpyxl, pandas available)
- [ ] T4.2 · Wire tool into the model's tool-calling interface
- [ ] T4.3 · Test: model can read, write, and manipulate .xlsx files end-to-end

### P5 — RAG (Personal Docs)

- [ ] T5.1 · Choose vector DB (Chroma/Qdrant/other), log in DECISIONS.md
- [ ] T5.2 · Build ingestion pipeline for personal docs/notes
- [ ] T5.3 · Wire retrieval into model context
- [ ] T5.4 · Test: model answers using uploaded document content

### P6 — Fine-Tuning Exploration

- [ ] T6.1 · Choose fine-tuning framework (Unsloth/Axolotl), log in DECISIONS.md
- [ ] T6.2 · Curate or generate training dataset (instruction/response pairs)
- [ ] T6.3 · Run LoRA fine-tune on the Windows box GPU
- [ ] T6.4 · Evaluate: compare base vs. fine-tuned on representative tasks

---

## R5. Future Phases (sketch)

- **P7 — Multi-user hardening:** per-user auth/settings in Open WebUI, usage logging, any husband-specific customization
- **P8 — Expansion:** additional tools, additional models, hardware upgrades if warranted

---

## R6. Backlog

- **WoL re-examination:** once P1/P2 is testable single-user, examine actual usage pattern — how often the box is idle vs. in use, whether always-on has meaningful power-consumption cost worth solving with WoL or scheduled sleep. Not before then (DECISIONS.md 2026-09-04)
- **System prompt library:** curated system prompts for different task types (coding, recipes, writing, data analysis) — not before P2 is working

---

## R7. Change Log

- `2026-09-04` — Docs restructured: PROJECT_RULES.md replaced by OPERATIONS_GUIDE.md (single source of truth for Claude Project instructions field). ROADMAP rewritten to R0–R7 format with status legend and task-level checklist. GLOSSARY.md created. DECISIONS.md, HANDOFF.md, PATCH_NOTES.md, ARCHITECTURE.md reformatted to match Good Macros doc standards. Section-sign character permanently retired (never appears in any Bueno doc). P0 tasks T0.1–T0.4 retroactively logged and closed
- `2026-09-04` — Networking decision (Tailscale) and WoL deferral logged in DECISIONS.md. Tailscale setup blocked on owner regaining physical access to Windows box (~7 days)
- `2026-09-04` — ROADMAP created, P0 opened
