---
date: 2026-03-20
series: Agents in the Wild
session: 5
venue: The Kannas, Chiang Mai
youtube: https://youtube.com/watch?v=KnYyoUgUK2Q
---

# Agents in the Wild — March 20, 2026

The 5th weekly session tracking the "Open Claw" phenomenon and agentic AI developments. In-person meetup with live stream.

## 1. Open Claw Explosion in China

The session opened with a major news item: reports from CNBC and Reuters claiming 100,000+ Open Claw instances had sprung up in China in a single week, with tens of thousands of citizens setting up their own instances and provincial governments launching official ones too. The group was initially sceptical about whether the numbers were real.

A participant messaged his Chinese business contacts in real time and got confirmation from five of them: three out of five companies were running multi-branch training programmes on Open Claw, across hardware, deep tech, and logistics sectors. There is widespread FOMO among the general public, and a dedicated symbol — a single Chinese character plus a lobster emoji, translating to "Rising Shrimp" — has become the cultural shorthand for the movement.

The group discussed Baidu's offering at $2.50/month, debating whether inference costs were included. The consensus was that if inference is included, it's remarkable given GPU constraints — though China's power capacity is roughly 10x the US, potentially allowing less optimal but more abundant hardware. There was also discussion about how China has historically been ahead on applied AI and super-apps, and how accessing reliable information about the Chinese market remains a challenge.

One participant noted you can simply change an iPad's App Store to Chinese and browse the top 100 apps to see what's happening — "it's not North Korea... we could fly there tonight."

## 2. Manis (Meta's Personal Agent)

Meta recently acquired Manis, which now offers a personal agent system that runs locally on your laptop. The group saw it as yet another entrant in the growing field of agent systems (alongside Open Claw, Nano Claw, Iron Claw, Termies, Paperclip, etc.).

Nobody had tried it. There was speculation it might just be a wrapper around Claude Code or a similar harness underneath. One participant noted Manis was originally a chat product built into Messenger years ago, so this may be a pivot. The key differentiator they noticed was the local-first approach, but the features ("build an app") looked identical to existing tools.

## 3. Google's A2A Protocol

Google re-released their Agent-to-Agent (A2A) communication protocol, which had originally launched the previous year with zero traction — unlike MCP servers, which went from nothing to 200,000+ in weeks.

This triggered the longest discussion of the session. The core question: **how should agents talk to each other?** Key points raised:

- **The problem is real:** People at these meetups regularly ask "can my agent talk to your agent?" but there's no agreed-upon standard for communication surface, interface, or permission boundaries.
- **Is it just APIs?** Several participants argued that agent-to-agent communication is functionally identical to HTTP API calls — "you don't know what's on the other side, whether it's deterministic or an AI." The Turing test analogy was invoked.
- **Remote tool use vs. agent chat:** The group distinguished between agents chatting (low practical value currently) and remote tool use (high value — "you have a tool I want to use").
- **Trust and identity:** How do you verify the agent on the other end is who it claims to be? Same problems as API authentication.
- **Pragmatic approach:** The presenter said he'd just go with whichever protocol gets the largest user base backing. Some suspected Google wants to be "the man in the middle" to charge fees, though the protocol itself appears to be an open spec (like an RFC).

## 4. Open Viking — Context Database for Agents

Briefly covered: Open Viking proposes a virtual file system paradigm for agent context, treating memories, resources, and capabilities as virtual directories under a protocol. It introduces tiered context loading (L0: ~100 tokens, L1: ~2K tokens, L2: full content) to reduce token consumption.

The presenter noted he does something similar himself — summarising per folder. This led into the session's deepest technical discussion.

## 5. The Drift Problem & Agent Language Specification

The presenter identified what he considers the central unsolved problem in personal agent systems: **structural drift**. When agents write files to directories over time, the schema of each file varies slightly. After a thousand files, searches break because legacy files are missing properties. This is why Open Claw users report burning millions of tokens on simple searches after two months of use.

**The root cause:** Unlike coding agents (which can self-verify via tests, linters, and browser checks), personal agent systems have no verification loops.

**His solution — Agent Language Specification:**

- A DSL (domain-specific language) that treats every directory as a database table and every markdown file as a row
- Front matter fields are strongly typed — all fields must be explicitly present (no optional fields), ensuring agents can search with confidence
- Enforces referential integrity between modules (like foreign keys in a relational database)
- A compiler validates every file against the schema after each write; if an agent adds non-conforming content, it fails with diagnostics
- Supports versioned schemas (v1, v2) with migration paths — agents can generate migration code automatically
- Entry point enforcement: agents must go through a "skill" (containing business logic as natural language) to interact with any directory — never writing directly

**Key design philosophy:** The "high-level language of the future" is natural language and architecture. Low-level concerns (classes, variables) are handled by coding agents. The system is self-service: a user can say "I want to start saving invoices" and the system asks clarifying questions, generates the schema, writes the skill, sets up hooks, and handles future migrations.

A participant raised the question of validating content within sections (not just structure). The presenter confirmed the compiler handles this via referential integrity checks — detecting broken pointers and dangling references.

Another participant noted he uses automations in skills instead of a compiler, but found the compiler approach compelling because it prevents drift even if the agent ignores instructions.

## 6. Claude Code Channels — Live Demo

The presenter demoed **Claude Code Channels**, released that same day (~10 hours prior). He set up a Telegram bot connected to a Claude Code instance running on a Fly.io VPS:

- **Setup:** Deployed Anthropic's official Claude Code Docker image to Fly.io, SSH'd in, installed the official Telegram plugin, and added a special flag to the Claude Code instance
- **How it works:** Messages sent via Telegram are forwarded to the Claude Code instance, which processes them and responds. The Claude Code instance acts as the server
- **Limitations discovered:**
  - If the Claude Code instance is killed, the bot dies — no background/daemon mode
  - Slash commands (compact, clear) don't work
  - No streaming — responses arrive as complete blocks
  - Only Telegram and Discord supported at launch
- **Architecture:** Uses SSE (Server-Sent Events) pushing to Claude Code. A participant asked if they could build their own version for Matrix or a web interface — the presenter believed this should be possible since it's based on MCP sampling

The group noted this appears to be Anthropic's response to the Open Claw phenomenon — letting users chat with their agent where they already chat, rather than requiring a dedicated app.

## 7. Sub-agents, Forking, and Context Management

The final discussion covered sub-agent patterns and context window management:

- **Sub-agents** spin up with fresh context, do work, and return only results — preserving the main window's context budget. "Do it in a sub agent" is becoming a common instruction
- **Codex** officially released sub-agents that week, with unlimited recursion depth (configurable via integer), versus Claude Code's single-level limit
- **Fork vs. Thread analogy:** The group debated Unix process metaphors:
  - Thread ≈ background agent (own context, runs in parallel)
  - Fork ≈ sub-agent with parent context copied over
  - The analogies break down since this is higher-level than OS processes
- **1M context window impact:** The upgrade from 200K to 1M has changed workflows — one participant said he used to clear context four times a day and now never does. However, most are still cautious beyond 200-300K tokens, not trusting recall accuracy for information deposited early in the window
- **Practical insight:** Accuracy is highest in the most recent ~10% of context. If you use forking (sub-agents with inherited context), you only ever operate in that fresh window, so total context depth matters less
