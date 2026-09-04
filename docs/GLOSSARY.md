# GLOSSARY

Canonical reference for every acronym, symbol prefix, ID pattern, and naming convention used across Bueno. When a document uses shorthand, this file is where the shorthand is defined. Update alongside any change to the naming systems.

Format: label — expansion (kind) — one-line meaning. Grouped by domain. Retired terms live at the bottom so they resolve for anyone reading historical docs.

---

## Roadmap and project structure

- **R#** — Roadmap section (R0 at-a-glance, R1 north star, R2 locked architecture, R3 constraints, R4 current phase, R5 future phases, R6 backlog, R7 change log). Only appears in and about `ROADMAP.md`
- **P0, P1, P2 … P8** — Phase. Project ladder from P0 (scaffolding) through P8 (expansion). See `ROADMAP.md` R4 for the current phase and R5 for future-phase sketches
- **T#.#** — Task within a phase (e.g. T1.3 = task 3 of Phase 1). Used in R4 task checklists
- **Rule N** — Numbered rule in `docs/OPERATIONS_GUIDE.md` (Rules 1–35). Always spelled `Rule N`, never a bare number
- **`session YYYY-MM-DD (hash)`** — Reference to a specific working session, by ISO date + short git commit hash of that session's first (or representative) commit. Forever standard for session references

## Technical

- **PAT** — Personal Access Token (GitHub). Provided fresh each session per Rule 9; the assistant cannot store tokens
- **LLM** — Large Language Model
- **RAG** — Retrieval-Augmented Generation. Feeding personal docs/notes into the model's context at query time
- **LoRA** — Low-Rank Adaptation. Parameter-efficient fine-tuning method runnable on a single consumer GPU
- **VRAM** — Video RAM. GPU memory; the bottleneck for local model size
- **WoL** — Wake-on-LAN. Remote power-on via network packet. Deferred (DECISIONS.md 2026-09-04)

## Paths

- **Mac dev path** — `~/Bueno` (`/Users/nali/Bueno`)
- **Windows inference host path** — TBD (set at P1 bring-up)
- **Repo** — `github.com/Talley2038/Bueno` (private)

---

## Retired terminology

(none yet)
