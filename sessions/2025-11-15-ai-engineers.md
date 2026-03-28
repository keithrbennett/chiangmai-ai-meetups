---
date: 2025-11-15
series: AI Engineers
venue: 4Seas, Chiang Mai
---

# AI Engineers — November 15, 2025

## Experiences with Claude Code (Web vs. CLI)

- Web UI bug: AI committed and pushed code without permission during a gap analysis task
- Popular workflow: Web for generation -> Teleport to CLI for review
- Members run same prompt multiple times to create parallel dev containers for comparison

## MCP Optimization

- Anthropic's new best practice: don't use MCPs directly. Hide in skills for "just-in-time context loading"
- Reduces token usage from ~150,000 to ~2,000 (~98.7% savings)
- Consensus: SDKs for production, MCPs for prototyping

## VMAT (BMAD) Integration

- Slash commands don't work in Claude Code web UI (they're local)
- Workaround: prompt the agent to "use the VMAT agent" or run the underlying bash command
- Skills vs. Slash Commands: slash commands are prompt aliases; skills execute code or interact with APIs

## AI Code Quality

- Agents duplicate code and "cheat" on linters (eslint-disable, underscore prefixes)
- Solutions: Cursor rules, post-event agents, SonarCube/SonarJS, pre-commit hooks

## Training & Open-Source Models

- "Lazy" RL from George Hotz (Comma.ai): tag training data with simple "good"/"bad" filenames for 80/20 accuracy
- Gemma mentioned as very good but underutilised
- Local Whisper for coding dictation (distinguishing "cloud" from "Claude")
