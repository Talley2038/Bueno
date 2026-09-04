# HANDOFF

**Repo tip:** `fe2adbf`
**Standing session-start steps:**
1. Read `docs/ROADMAP.md` R1-R3 and R0, and this file, before proposing work (Rule 1)
2. Skim `docs/GLOSSARY.md` if any symbol/acronym is unfamiliar

---

## Where we are

**P0: closing this session.** T0.1-T0.4 done. Docs restructured, decisions locked, repo scaffolded.

**What exists right now:**
- Repo at `github.com/Talley2038/Bueno` (private) with full doc set
- No code, no config, no running software

---

## Next-steps (priority order)

### 1. P1 bring-up: blocked on physical access (~2026-09-11)
Install Ollama + Tailscale on the Windows box, pull first model pair, confirm reachable from Mac. See R4 T1.1-T1.5.

### 2. P2 chat interface: after P1
Open WebUI connected to the Ollama endpoint. See R4 T2.1-T2.3.

---

## Known open items

- No physical access to the Windows inference host for ~7 days (only real blocker)
- Model pair selection (leaning Qwen2.5-Coder 14B + Qwen2.5 14B) is a strong candidate but not locked. Decision logged at T1.5, not before

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
