# ARCHITECTURE.md

Clarity over terseness in this file — audience includes future engineers
(Rule 14 exemption).

## Overview
Bueno is a local-first LLM assistant. It has two machines in its topology:

- **Windows desktop** ("the inference host"): runs Ollama, serves an
  OpenAI-compatible API over the LAN. Has the only GPU (RTX 5070, 12GB
  VRAM) in the setup.
- **Mac** ("the dev/client machine"): where development happens, and
  where the chat frontend (Open WebUI) is used day-to-day.

## Target OSes
- Windows desktop: Windows 11, cmd.exe/PowerShell
- Mac: macOS, zsh/bash

Code and scripts that run on both must be tested on both; scripts specific
to one host are labeled clearly by directory or filename.

## Components
- **Inference server**: Ollama, running on the Windows box. [NOT BUILT]
- **Chat frontend**: Open WebUI, connecting to the Ollama endpoint over
  LAN. [NOT BUILT]
- **Web search tool**: TBD (SearXNG self-hosted vs. Brave Search API).
  [NOT BUILT]
- **Excel/code execution tool**: Python sandbox with openpyxl/pandas,
  exposed as a callable tool to the model. [NOT BUILT]
- **RAG layer**: TBD, likely a local vector DB (Chroma/Qdrant) over
  personal docs/notes. [NOT BUILT]
- **Fine-tuning pipeline**: LoRA via Unsloth or Axolotl, run on the
  Windows box's GPU. [NOT BUILT]

## Network
Mac talks to the Windows box's Ollama API over the LAN. Exact addressing
(static IP, hostname, or Tailscale) — open question, see HANDOFF.md.
