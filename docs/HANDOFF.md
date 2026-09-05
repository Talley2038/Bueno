# HANDOFF

**Repo tip:** `ca83805`
**Standing session-start steps:**
1. Read `docs/ROADMAP.md` R1-R3 and R0, and this file, before proposing work (Rule 1)
2. Skim `docs/GLOSSARY.md` if any symbol/acronym is unfamiliar

---

## Where we are

**P0: open.** T0.1-T0.5 done (repo, docs, decisions, voice pass, rule amendment). T0.6-T0.9 are open and doable right now from Mac, no desktop needed.

---

## Next-steps (priority order)

### 1. T0.6: Tailscale account + Mac install
Create account, install on Mac, confirm `tailscale status` shows the Mac as a node.

### 2. T0.7: Model research
Benchmark candidate models (Qwen2.5-Coder 14B, Qwen2.5 14B, Qwen3, DeepSeek-R1-Distill) against the 12GB VRAM constraint. Write up recommendation in DECISIONS.md.

### 3. T0.8: System prompt v1
Draft the system prompt that shapes the local model's behavior (coding style, recipe reasoning, tone, tool-call conventions). Save as `config/system_prompt_v1.md`.

### 4. T0.9: Fine-tuning dataset format
Design the JSONL schema, sourcing strategy, and target volume. Save as `data/README.md`.

### 5. P1: blocked on desktop access (~2026-09-11)
Everything in P1 requires the Windows box.

---

## Known open items

- No physical access to the Windows desktop for ~7 days (blocks P1, does NOT block T0.6-T0.9)

---

## Standing close-out step (Rule 11)

**Mac (zsh):**
```
cd ~/Bueno && git pull
```

**Windows (cmd):**
```
cd C:\path\to\Bueno
git pull
```

---

## Credentials for next session

Generate a fresh fine-grained PAT at `https://github.com/settings/tokens` with:
- Repository access: `Talley2038/Bueno`
- Permissions: Contents Read and write, Metadata Read-only (auto)
