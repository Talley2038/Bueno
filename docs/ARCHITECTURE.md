# ARCHITECTURE

**Status:** Canonical design document
**Last updated:** 2026-09-04

Clarity over terseness in this file (Rule 14 exemption).

---

## 1. Purpose

Bueno is a private, locally-run LLM assistant. No cloud inference. No central server beyond a single household machine. Two machines in the topology, connected via Tailscale.

## 2. Design Principles

- **Local-first.** Inference runs on hardware under direct physical control. No data leaves the LAN except explicit tool calls (web search)
- **Minimalism earns its place.** Standard tools first. Dependencies justified and logged (Rule 16)
- **Idempotent operations.** Re-running anything is always safe (Rule 24)
- **Portable paths.** All file access via `pathlib.Path`. No machine-specific paths hardcoded

## 3. Topology

```
+---------------------------------------------------+
| WINDOWS DESKTOP (inference host)                   |
|  OS: Windows 11, cmd.exe / PowerShell              |
|  GPU: RTX 5070, 12GB VRAM                          |
|  RAM: 32GB DDR5-6000                               |
|  CPU: Ryzen 7 9700X (8C/16T)                       |
|  Storage: 2TB NVMe                                 |
|                                                    |
|  Ollama (inference server)          [NOT BUILT]    |
|  Tailscale (mesh node)              [NOT BUILT]    |
+------------------------+---------------------------+
                         | Tailscale mesh (encrypted)
+------------------------+---------------------------+
| MAC (dev / client machine)                         |
|  OS: macOS, zsh                                    |
|                                                    |
|  Open WebUI (chat frontend)         [NOT BUILT]    |
|  Tailscale (mesh node)              [NOT BUILT]    |
|  Dev tools (git, python, editor)                   |
+------------------------+---------------------------+
                         | Tailscale mesh
+------------------------+---------------------------+
| ADDITIONAL DEVICE(S)                               |
|  Open WebUI (browser)               [NOT BUILT]    |
|  Tailscale (mesh node)              [NOT BUILT]    |
+---------------------------------------------------+
```

## 4. Components

| Component | Tech | Status |
|---|---|---|
| Inference server | Ollama | [NOT BUILT] |
| Chat frontend | Open WebUI | [NOT BUILT] |
| Web search tool | TBD (SearXNG or Brave API) | [NOT BUILT] |
| Excel/code execution tool | Python sandbox (openpyxl, pandas) | [NOT BUILT] |
| RAG layer | TBD (Chroma/Qdrant) | [NOT BUILT] |
| Fine-tuning pipeline | TBD (Unsloth/Axolotl), LoRA | [NOT BUILT] |

## 5. Network

All inter-machine communication routed through Tailscale. Each device gets a stable Tailscale hostname. No ports opened on the home router. No direct internet exposure of the inference server.

Open WebUI serves its frontend locally on whichever device is in use, connecting to the Ollama API at `http://<windows-tailscale-hostname>:11434`.

## 6. Target Environment

- **Windows desktop:** Windows 11, `cmd.exe` primary (PowerShell available). `python` (not `python3`)
- **Mac:** macOS, zsh/bash. `python3`
- **Sandbox (assistant):** Linux. Code and tests must work on all three
