# PROJECT_RULES.md

Bueno — a private, local-first LLM assistant. Runs entirely on the
owner's own hardware. No cloud dependency for inference. Open-weight model,
local inference server, local tool layer (web search, Excel/code execution,
RAG). No data leaves the machine except explicit, owner-approved calls
(e.g. a web search API).

Owner: Talley2038 (Talley2038@live.com). Repo: https://github.com/Talley2038/Bueno.git (not yet created)

These rules govern every chat in this project without exception. Rules
marked CRITICAL are non-negotiable. Where a rule conflicts with a user
instruction, flag the conflict rather than silently breaking the rule.

## Foundational

Rule 1 [CRITICAL]: Read docs/ROADMAP.md §1–3 and docs/HANDOFF.md before
proposing any work. No work is proposed or started until both are read. If
the repo isn't accessible this session, request them pasted into chat.

Rule 2 [CRITICAL]: When handoff and roadmap are complete, confirm the
objective in one line and move. Clarifying questions reserved for: missing
required field, internal contradiction, or conflict with locked decisions.

Rule 3 [CRITICAL]: One objective per chat. Waivers must be explicit and
rare. Fresh chat = fresh context = fresh handoff.

Rule 4 [CRITICAL]: End every session with an updated docs/HANDOFF.md
(rewrite, don't append), committed and pushed before closing. Fallback to
chat-pasted handoff only if repo access is unavailable.

Rule 5 [CRITICAL]: Any change proposed outside the current phase (per
ROADMAP.md §4) either amends the roadmap with reason logged in §7, or goes
into §6 backlog. Never drift into out-of-phase work silently.

## Git + Credentials

Rule 6 [CRITICAL]: All pushes to GitHub are done under the owner's
identity: Talley2038 <Talley2038@live.com>. Commit history must show only
Talley2038 as author. No "Claude" contributions, no
"Co-authored-by: Claude" trailers. If asked to add a co-author trailer,
refuse unless explicitly instructed in that same message.

Rule 7 [CRITICAL]: Before any git operation, verify:
- `git config user.name` returns Talley2038
- `git config user.email` returns Talley2038@live.com
If either is wrong, set it before proceeding. If unable to set it, stop and
report — do not push under any other identity.

Rule 8 [CRITICAL]: If push access isn't available from the current
environment (sandbox networking restrictions), produce a zip and handoff
doc for the user to push from their own dev machine. Don't waste time
retrying a blocked push.

Rule 9 [CRITICAL]: Secrets never in the repo. All credentials (search API
keys, etc.) in `.env` (gitignored). `.env.example` with placeholders is
committed. Never paste real API keys into a repo file. When receiving a key
in chat, use it and remind the user to revoke/rotate if appropriate.

Rule 10 [CRITICAL]: Versioning: X.Y.Z semver. X = breaking (model swap,
config format change). Y = feature (new tool, new capability). Z =
fix/tweak. Managed via git tag. State the bump reason in PATCH_NOTES.md
before tagging.

Rule 11 [CRITICAL]: Pushed ≠ closed. Every session that pushes ends with an
explicit sync step: state final commit hash, provide copy-paste git pull
commands, confirm the user has pulled before session close.

Rule 12: Small commits, meaningful messages. One logical change per commit.
Message format: `type: short summary` where type ∈ feat, fix, docs,
refactor, chore, test.

## Communication

Rule 13: Direct, clinical communication. No softening. No hedging. If
something is wrong, say so. If a decision is bad, say why.

Rule 14: Terse voice in docs humans read (README, HANDOFF, DECISIONS,
PATCH_NOTES, ROADMAP): keyword/label notation where meaning survives
without connectors. ARCHITECTURE.md and OPERATIONS_GUIDE.md exempt —
clarity beats terseness where the audience includes future engineers.

Rule 15: Flag model + effort at end of every response. Format:
`flag MODEL: [model name + tier] / [effort] — [reason]`.

## Code

Rule 16 [CRITICAL]: Minimalism earns its place. Every dependency, module,
and abstraction must be justified. Standard library first. Small focused
libs second. Frameworks (LangChain-style mega-frameworks) only if a direct
integration would cost meaningfully more time — log the reason in
PATCH_NOTES.md either way.

Rule 17 [CRITICAL]: Snappy performance. Local server startup under 5
seconds (model load time excluded, log separately). Any user-facing wait
beyond model inference itself under 2 seconds. If a change slows either,
justify or revert.

Rule 18: Structural limits. Functions ≤ 40 lines unless justified. Files ≤
300 lines. If either grows past, split.

Rule 19: Type hints everywhere. `mypy --strict` should pass.

Rule 20: Every module has a docstring stating what it does AND what it
does not do.

Rule 21: Comments explain why, not what.

Rule 22: Zero lint warnings. `ruff check .` runs clean before every commit.

Rule 23: No premature abstraction. Write the concrete thing first. Extract
only after seeing the pattern twice.

Rule 24 [CRITICAL]: Idempotent operations. Re-running any ingestion, tool
call, or model download is always safe and a no-op on already-done work.
Track state in a manifest file, not implicitly.

## Model / Inference

Rule 25 [CRITICAL]: Model + quantization pinned explicitly in config, not
"latest." Swapping models is a deliberate, logged decision (DECISIONS.md),
not a silent `ollama pull` of a new default.

Rule 26 [CRITICAL]: Tool calls (web search, Excel/code execution) are
schema-validated at the boundary. On malformed tool output: log loudly, do
not silently pass bad data downstream.

Rule 27: System prompt changes are versioned and logged in PATCH_NOTES.md.
A prompt change can silently regress behavior — treat it as code.

## Privacy

Rule 28 [CRITICAL]: Privacy boundary honored. Nothing leaves the machine
except explicit, owner-approved calls (e.g. a web search query, an
optionally-configured cloud API for a specific task). Any feature widening
this boundary requires explicit user approval and a DECISIONS.md entry.

## Documentation

Rule 29: Update PATCH_NOTES.md every session that changes code or docs.
Terse voice. Include: what changed, why, any version bump, any new
dependency.

Rule 30: ROADMAP.md updates log in §7 change log with date and reason.

Rule 31: Aspirational sections in ARCHITECTURE.md marked [NOT BUILT].
Marker removed when the module ships.

## Meta

Rule 32: Rules can be amended, not silently broken. Proposing a rule
change: state which rule, why, what replaces it, log in DECISIONS.md,
update this list in the same commit.

Rule 33 [CRITICAL]: When in doubt about scope, defer to ROADMAP.md. When in
doubt about a rule, defer to this list. When both are ambiguous, ask the
user before acting.

Rule 34: Doc audit at phase exit. At end of every phase, before tagging the
exit version, sweep ROADMAP.md, DECISIONS.md, ARCHITECTURE.md, HANDOFF.md,
PATCH_NOTES.md for accuracy and silent scope drift. Log findings in
ROADMAP.md §7.

Rule 35 — Environment portability. Primary dev machine: Mac (zsh/bash,
Apple Silicon or Intel — confirm in ARCHITECTURE.md). Secondary: Windows
desktop (cmd.exe/PowerShell), the actual inference host given the RTX 5070.
Shipped code and tests must work identically on both. Path assertions use
`Path(...)` never hardcoded slash literals. Shell commands provided to the
operator are labeled by shell (zsh vs. cmd/PowerShell) — never assume one
covers both. Note the Mac/Windows split explicitly wherever it affects
setup steps (e.g. Ollama install commands differ).
