---
date: 2026-03-13
series: Agents in the Wild
venue: The Kannas, Chiang Mai
duration: 2h 15m
speakers: 8
---

# Agents in the Wild -- March 13, 2026

A long Friday session dominated by three substantial discussions: agent security and tool agnosticism, the Paperclip control plane for multi-agent orchestration, and a group debate on orchestration tools. Geo coordinates on the first segment place the start at The Kannas.

---

## 1. Agent Security and Tool Agnosticism

A small group of developers shared how they structure and secure AI agents across different providers:

**Skills portability problem:**
- Keeping separate skill files per model (Claude vs Codex) makes practical sense because Anthropic-specific features -- context forking, sub-agents, preprocessor directives (`!` commands) -- are not portable to standard agent formats.
- One developer has distinct `claude.md` and `agents.md` in their repo root, with completely different content. Codex handles code; Claude handles life management and agent orchestration.
- The goal is to stay as LLM- and tool-agnostic as possible to make migration easier when providers change or have outages.

**Secrets management:**
- One participant keeps API keys in a private GitHub repo for convenience. Others advocated for 1Password vaults with narrowly scoped service accounts, so each agent or skill exposes only a single limited key if compromised.
- Pattern described: agents retrieve credentials at runtime via `op run` (1Password CLI). The operational overhead is significant -- many service accounts, scopes, and keys to create and document -- but the security posture is far better than scattered `.env` files.
- Keys ultimately transit through Anthropic/OpenAI when used, which is an accepted risk.

**CLIs vs raw APIs:**
- Some have built custom CLIs for Google services (Gmail, Calendar, Analytics, Search Console, marketing metrics). CLIs are token-efficient and ergonomic.
- The trend is toward raw HTTP/JSON API calls documented directly in skill files. CLIs add layers that break when APIs change; JSON payloads keep agents closer to the underlying APIs.
- Paragon was mentioned as an aggregation layer for multiple data sources (Google Analytics, Ads, Meta, etc.).

---

## 2. Paperclip Control Plane and Telemetry

The longest segment of the session. Participants discussed advanced agent orchestration, telemetry, and the Paperclip tool in depth:

**Telemetry and session intelligence:**
- A participant demonstrated a system that captures and summarises every agent conversation transcript, building reflection and audit capabilities over JSONL logs.
- Session captures are scoped by project and subsystem, enabling development subsystems to enforce complete audit trails.
- Five variations of session-capture skills exist, each tailored to different workflows.

**Skill management at scale:**
- The group compared strategies for syncing large skill collections across machines: Markdown files vs databases (MongoDB), Git + cloud storage, FreeFileSync, virtual file systems via FUSE.
- Portability between harnesses and machines remains painful, particularly around prompt-injection risks when skills reference external content.

**Paperclip walkthrough:**
- Paperclip is an orchestration/control-plane tool that models organisations (CEO, founding engineer, hierarchy) and runs agents via subprocess adapters (Claude Code, Codex, Gemini).
- Workflow: set up a company, auto-hire agents, create projects and issues, track costs. Paperclip communicates via fire-and-forget subprocesses with JSONL logs and uses issue comments as pseudo-sessions.
- A real-world case was shared where Paperclip-driven agents autonomously created blogs, launch strategies, social posts, screenshots, and deployments, with human oversight only for API keys and risky actions.
- **Anthropic Max subscription constraints:** Using local subprocesses counts against the subscription, but distributed SDK usage does not -- an important distinction for scaling.

**Publishing session materials:**
- The group discussed making transcripts and slides available via a shared GitHub repo, and plans for future hardware (cameras, live streaming) and integration with a "ghost" system so agents can consume and summarise events.

---

## 3. Agent Orchestration Tools Landscape

A group review of the rapidly emerging orchestration and control-plane space:

**Tools surveyed:**
- **Paperclip:** Organisational model with hierarchical agent roles (covered in detail above).
- **TMux IDE:** Highly opinionated, developer-only workflow for Claude swarms running in terminal multiplexer panes.
- **Demux:** Spawns many agents in terminal panes but forces manual steering and review.
- **Conductor, Codex, OpenAI Symphony:** Referenced as additional entrants in the space.

**Key debates:**
- **Transparent vs black-box UIs:** Some prefer seeing all agent progress to intervene when things go off track. Others want systems that hide internal activity to reduce cognitive load and anxiety.
- **Illusion of productivity:** Spinning up many agents doing redundant work feels productive but may not be. The facilitator warned about confusing parallel execution with actual progress.
- **Multi-agent failure modes:** Agents rewriting each other's work, looping, or devolving into circular conversations were common complaints.
- **Task management integration:** The group discussed how agents might auto-generate and sequence tasks using Kanban boards (Linear, GitHub Issues, Notion, Airtable) or file systems. Claude Opus was noted as particularly good at ordering implementation steps.

**Provider anxiety:**
- Multiple participants described constant worry about hitting API limits, getting banned, or having subscriptions terminated. Every notification from Anthropic triggers a moment of panic.
- Strategies for managing costs: offloading cron-style ingestion jobs to cheaper models (Gemini, local LLMs) rather than burning Opus or Sonnet tokens.

---

## 4. Automating Event Discovery

A short segment where participants discussed pulling event information automatically from the Luma/Loma platform. Questions raised: does Luma have an API? Can an RSS feed be set up so an AI agent can retrieve event dates and locations on demand? The desire is to ask your personal agent about upcoming meetup details rather than manually checking group links.

---

*Session recorded during the Agents in the Wild Friday meetup in Chiang Mai, March 13, 2026.*
