# ROADMAP.md

## §1 Objective
Private, local-first LLM assistant. Windows desktop (RTX 5070, 12GB VRAM)
as inference host. Mac as primary dev/client machine. Coding help, recipe
generation, web-search-augmented answers, Excel automation, general
assistant work — no cloud dependency for inference, no data leaving the
LAN except explicit tool calls (web search).

## §2 Constraints
- Inference host: Windows desktop, RTX 5070 12GB VRAM, Ryzen 7 9700X, 32GB
  DDR5
- Dev machine: Mac (primary, current focus)
- Target model class: 7B–32B open-weight, 4-bit quantized
- Owner: Talley2038

## §3 Non-goals
- Not attempting to replicate a frontier hosted model's reasoning depth
- Not training from scratch
- No multi-user / public-facing deployment

## §4 Current phase
**Phase 0: Scaffolding** — repo structure, docs, no code yet.

## §5 Phase plan
- Phase 0: Scaffolding (this phase)
- Phase 1: Inference host bring-up — Ollama on Windows box, model pulled,
  reachable over LAN from Mac
- Phase 2: Chat interface — Open WebUI connected to Ollama endpoint
- Phase 3: Web search tool integration
- Phase 4: Excel/code execution tool (Python sandbox, openpyxl/pandas)
- Phase 5: RAG (personal docs/notes)
- Phase 6: Fine-tuning exploration (LoRA, style/behavior adaptation)

## §6 Backlog
(empty)

## §7 Change log
- <date TBD>: ROADMAP created, Phase 0 opened
