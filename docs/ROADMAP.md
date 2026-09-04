# ROADMAP

Canonical scope + phase map + task-level status. Read R1-R3 at the start of every session; read R0 always.

**Status legend:** 
`[ ]` open  

`[~]` in progress  

`[x]` done   

`[!]` blocked 

**Format:** 
`- [x] ID · Description (testable done-state) 
started YYYY-MM-DD 
done YYYY-MM-DD · vX.Y.Z`
Version tag only when the item lands with a bump.

---

## R0. At-a-glance

- **Phase:** **P0 OPEN** (scaffolding + pre-desktop prep)
- **Version:** `v0.1.0` (initial scaffold)
- **Repo:** https://github.com/Talley2038/Bueno (private)
- **Current milestone:** P0 tasks T0.5-T0.8 (doable now from Mac, no desktop needed)
- **Active blockers:** P1 blocked on physical access to Windows desktop (~2026-09-11). P0 is NOT blocked
- **Last audit:** None yet (first phase)

---

## R1. North Star

Build and maintain Bueno (a private, locally-run LLM assistant that runs entirely on local hardware). Windows desktop hosts inference via Ollama; Mac is the occasional dev/client machine. Accessible from anywhere via Tailscale. Two planned users.

Capabilities: coding help, recipe generation, web-search-augmented answers, Excel/data automation, general assistant work. No cloud dependency for inference. No data leaves the LAN except explicit tool calls (web search API).

---

## R2. Locked Architecture

Non-negotiable unless explicitly reopened in `DECISIONS.md`.

- **Inference server:** Ollama on the Windows desktop (RTX 5070, 12GB VRAM)
- **Model class:** 7B-32B open-weight, 4-bit quantized. Model + quantization pinned explicitly (Rule 25)
- **Chat frontend:** Open WebUI connected to Ollama endpoint over Tailscale
- **Network:** Tailscale mesh connecting all devices
- **Privacy boundary:** nothing leaves the machine except explicit, approved tool calls (Rule 28)
- **Repo:** single private repo, `github.com/Talley2038/Bueno`

---

## R3. Constraints

1. Inference host GPU: RTX 5070, 12GB VRAM. Caps model size at ~14B fully on-GPU or ~32B with CPU offload
2. Dev machine: Mac (current primary). Inference host: Windows desktop
3. Primary dev machine is frequently remote. Tailscale is mandatory, not optional
4. Two planned users, both from arbitrary locations
5. No cloud inference dependency. Local model only
6. Windows box intended to run ~24/7 once operational

---

## R4. Current Phase: P0 Scaffolding + Pre-Desktop Prep

### Completed

- [x] T0.1 · Repo created and initial scaffold pushed · 2026-09-04
- [x] T0.2 · Networking decision locked (Tailscale) · 2026-09-04
- [x] T0.3 · WoL deferred to backlog with re-examine trigger · 2026-09-04
- [x] T0.4 · Docs restructured to R0-R7, OPERATIONS_GUIDE, GLOSSARY · 2026-09-04
- [x] T0.5 · Doc voice pass (em dashes, third-person language, terseness) · 2026-09-04

### Open (no desktop needed)

- [ ] T0.6 · Create Tailscale account and install Tailscale on Mac. Done when: `tailscale status` shows the Mac as a node
- [ ] T0.7 · Model research: benchmark Qwen2.5-Coder 14B, Qwen2.5 14B, Qwen3, DeepSeek-R1-Distill against hardware constraints (12GB VRAM). Done when: recommendation written up in `docs/DECISIONS.md` with model name, parameter count, quantization, and expected VRAM usage. Final lock deferred to T1.5 (needs real testing)
- [ ] T0.8 · Draft v1 system prompt for the local model (coding style, recipe reasoning, tone, tool-call conventions). Done when: `config/system_prompt_v1.md` exists in repo, version-logged per Rule 27
- [ ] T0.9 · Design fine-tuning dataset format and folder structure. Done when: `data/README.md` exists describing the JSONL schema, sourcing strategy (exported chats, synthetic generation, public datasets), and target volume

**P0 gate:** T0.1-T0.9 all closed. Decisions documented. System prompt drafted. Dataset format defined. Ready to begin P1 the moment desktop access is available.

---

### P1: Inference Host Bring-up [!] blocked on desktop access (~2026-09-11)

- [!] T1.1 · Install Ollama on Windows box. Done when: `ollama serve` responds on `localhost:11434`
- [!] T1.2 · Install Tailscale on Windows box, join same tailnet as Mac. Done when: `tailscale ping <mac-hostname>` succeeds from Windows and vice versa
- [!] T1.3 · Pull candidate model(s) per T0.7 recommendation. Done when: `ollama run <model>` produces a coherent response locally on the box
- [!] T1.4 · Confirm Ollama API reachable from Mac over Tailscale. Done when: `curl http://<windows-tailscale-hostname>:11434/api/generate` returns a response from the Mac
- [!] T1.5 · Lock model + quantization in config after real-world testing on the hardware. Done when: `config/model.yaml` specifies model name + quant, logged in DECISIONS.md
- [!] T1.6 · Configure Ollama to start on boot / run as service. Done when: Windows box can reboot and Ollama is serving without manual intervention

**P1 gate:** model inference running on the Windows box and reachable from the Mac over Tailscale. Model pinned. No manual steps required after a reboot.

---

### P2: Chat Interface

- [ ] T2.1 · Install Open WebUI. Done when: web UI loads in a browser at `http://localhost:8080` (or equivalent)
- [ ] T2.2 · Connect Open WebUI to the Ollama endpoint over Tailscale. Done when: a prompt sent through the UI returns a model response
- [ ] T2.3 · Configure multi-model switching (coder vs. generalist). Done when: can switch models mid-session in the UI and get responses from each
- [ ] T2.4 · Test from a second device over Tailscale. Done when: another device on the tailnet can load the UI and get a response
- [ ] T2.5 · Document the access pattern (URL, any auth) in OPERATIONS_GUIDE or a new `docs/USER_GUIDE.md`

**P2 gate:** two users can reach the chat UI from arbitrary locations via Tailscale, switch between models, and hold conversations.

---

### P3: Web Search Tool

- [ ] T3.1 · Evaluate search backends (SearXNG self-hosted vs. Brave Search API vs. others). Done when: decision logged in DECISIONS.md with reasoning
- [ ] T3.2 · Install/configure chosen search backend. Done when: search queries return results from the configured backend
- [ ] T3.3 · Wire search into Open WebUI as a tool. Done when: toggling "web search" in the UI causes the model to query the backend and incorporate results
- [ ] T3.4 · Test: ask a question requiring current information, verify the model searches and cites. Done when: a screenshot or log shows search-augmented response

**P3 gate:** model can search the web mid-conversation and incorporate results. Privacy boundary (Rule 28) documented for the search backend's data handling.

---

### P4: Excel / Code Execution Tool

- [ ] T4.1 · Design the tool-call interface (how the model invokes code execution, what sandbox it runs in, how results return). Done when: interface spec documented in `docs/ARCHITECTURE.md`
- [ ] T4.2 · Build Python execution sandbox with openpyxl and pandas available. Done when: a test script can read an .xlsx, manipulate it, and write output
- [ ] T4.3 · Wire sandbox as a callable tool in the model's tool-calling config. Done when: model can be prompted to "read this spreadsheet and add a column" and it executes
- [ ] T4.4 · Test end-to-end: upload .xlsx via Open WebUI, ask the model to transform it, verify output file. Done when: a real spreadsheet task completes successfully
- [ ] T4.5 · Validate tool output against schema (Rule 26). Done when: malformed tool output triggers a logged error, not silent pass-through

**P4 gate:** model can read, write, and manipulate Excel files via tool calls. Schema validation in place. A non-trivial spreadsheet task (pivot, formula generation, data cleanup) completes end-to-end.

---

### P5: RAG (Personal Docs)

- [ ] T5.1 · Evaluate vector DBs (Chroma, Qdrant, other). Done when: decision logged in DECISIONS.md
- [ ] T5.2 · Build ingestion pipeline: take a folder of docs (PDF, txt, md), chunk, embed, store. Done when: a test corpus is indexed and queryable
- [ ] T5.3 · Wire retrieval into the model's context (Open WebUI RAG feature or custom). Done when: model answers a question using content from an uploaded document that isn't in its training data
- [ ] T5.4 · Test with a real personal document. Done when: model correctly references specific content from a personal doc

**P5 gate:** personal documents are indexed and retrievable. Model answers questions grounded in uploaded content.

---

### P6: Fine-Tuning Exploration

- [ ] T6.1 · Evaluate fine-tuning frameworks (Unsloth, Axolotl, other). Done when: decision logged in DECISIONS.md
- [ ] T6.2 · Prepare training dataset per T0.9 format (minimum 200 high-quality instruction/response pairs). Done when: `data/training.jsonl` exists and passes schema validation
- [ ] T6.3 · Run LoRA fine-tune on the Windows box GPU. Done when: training completes without error and produces adapter weights
- [ ] T6.4 · Merge adapter into base model and serve via Ollama. Done when: `ollama run bueno-tuned` responds
- [ ] T6.5 · Evaluate: run the same 20 representative prompts against base and fine-tuned, compare. Done when: comparison written up in DECISIONS.md with a keep/revert/iterate call

**P6 gate:** fine-tuned model evaluated against base. Decision made on whether to use it as default.

---

## R5. Future Phases (sketch)

- **P7: Multi-user hardening:** per-user auth/settings in Open WebUI, usage logging, any user-specific customization
- **P8: Expansion:** additional tools, additional models, hardware upgrades if warranted

---

## R6. Backlog

- **WoL re-examination:** once P1/P2 is testable single-user, examine actual usage pattern: how often the box is idle vs. in use, whether always-on has meaningful power-consumption cost worth solving with WoL or scheduled sleep. Not before then (DECISIONS.md 2026-09-04)
- **System prompt library:** curated system prompts for different task types (coding, recipes, writing, data analysis). Not before P2 is working
- **Modelfile management:** Ollama Modelfile(s) versioned in repo for reproducible model config. Not before T1.5

---

## R7. Change Log

- `2026-09-04`: P0 expanded with pre-desktop tasks (T0.6-T0.9). All phases given testable done-states per task. Phase gates defined. Backlog item added (Modelfile management)
- `2026-09-04`: Doc voice pass: em dashes, third-person language, and section signs permanently removed from all docs
- `2026-09-04`: Docs restructured: PROJECT_RULES.md replaced by OPERATIONS_GUIDE.md. ROADMAP rewritten to R0-R7 format. GLOSSARY.md created. P0 tasks T0.1-T0.4 retroactively logged and closed
- `2026-09-04`: Networking decision (Tailscale) and WoL deferral logged in DECISIONS.md. Tailscale setup blocked on regaining physical access to Windows box (~7 days)
- `2026-09-04`: ROADMAP created, P0 opened
