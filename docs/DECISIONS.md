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
