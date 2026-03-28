---
date: 2026-01-31
series: AI Engineers
venue: 4Seas, Chiang Mai
duration: 2h 13m
speakers: 14
---

# AI Engineers -- January 31, 2026

Scheduling mishap forced the group back to 4Seas after the organiser forgot to book the preferred room (The Kannas). No projector available, so the planned lightning talk was dropped. Several new faces. The session was dense -- covering Kimi K2.5, MCP evolution, skill architecture patterns, agents.md compression, Claude Bot/Open Claude security, and prompt injection.

---

## 1. Logistics & Upcoming Claude Code Event

The organiser explained the venue switch and confirmed:

- **Next week (Feb 7):** No regular Saturday meetup. Instead, the Claude Code event at CMU Step, an official Anthropic-sponsored gathering. Doors at 10:00, starts at noon. Registrations still open.
- **Following week:** Intend to book The Kannas as the permanent Saturday venue.
- The session format remained open discussion since the room lacked a display for presentations.

---

## 2. Kimi K2.5 -- Open-Source Reaching Frontier Level

Kimi K2.5 from Moonshot (Chinese company) launched and generated significant buzz. One participant tested it extensively on conceptual reasoning tasks (not code):

- **Quality:** Comparable to Opus or Gemini 3 Pro at its peak. When fed complex compressed knowledge bases with many interrelated concepts, it automatically dissected them, critiqued weak assumptions, and pushed back with sophisticated reasoning. "I felt that vibe" of frontier-level performance.
- **Cost:** Roughly one-fifth to one-tenth of frontier model pricing, though exact per-token cost through third-party routers was unverified.
- **Swarm training:** The model was reportedly pre-trained for swarm capabilities -- rewarded during training for splitting tasks into parallel execution when beneficial and reverting to sequential when parallelism would break. This feature was not yet publicly released but was described as an internal capability baked into the weights.
- **Harness dependency:** True swarm execution requires the harness to provide spawn/worker tools. Some people were already running hacked versions of Claude Code with swarm features enabled via hidden beta flags and binary modifications.

**China's AI doctrine:** The group analysed why China is leading open-source model releases:

- **Chip constraints:** China is compute-poor relative to US labs. Open-sourcing models means Western companies host inference, offloading the GPU bottleneck.
- **Practical focus:** Rather than chasing AGI, Chinese labs focus on making AI work in factories, hospitals, and real-world systems. This means investing heavily in harness architecture and tooling.
- **Distillation pipeline:** Deep Seek was rumoured to be a distillation of GPT. Gemini's weights allegedly leaked and were used to accelerate open-source development. One participant noted that swarm capabilities "show up in Gemini now because they already exist inside Claude -- they're just not turned on" -- implying the leaked weights enabled reverse-engineering of unreleased features.

---

## 3. MCP UI Extension & the Decline of MCP Relevance

MCP received an official UI/frames extension allowing tool creators to send rendered UI components to the host application (custom tables, interactive cards, filters) instead of letting each harness format the output differently.

- **How it works:** A new "frame" concept in the MCP sequence diagram allows embedding UI elements in tool responses, similar to Slack bot cards or Teams interactive messages.
- **Community origin:** A community-generated MCP UI standard already existed; this was just the official adoption by the foundation (MCP was donated to the Linux Foundation alongside skills).
- **Room temperature: cold.** The group showed little interest. One participant summarised: "MCPs are not as useful as they were half a year ago." The developer community has shifted toward CLI-based skills.

---

## 4. Skills vs. MCPs -- Architecture Deep Dive

A long discussion on why skills are winning over MCPs in developer workflows:

**The MCP problem:** Developers tend to dump entire API surfaces into MCP containers (every Supabase function, for example). This creates a bloated tool list that confuses the LLM. What consumers actually want is opinionated, curated workflows -- the 80/20 of what people actually do, chained into routines.

**Skills advantages:**

- More token-efficient (only name + description loaded into context by default, not the full tool schema).
- CLI wrappers reduce LLM confusion. One participant wraps complex tools into simple commands (`start`, `stop`, `restart`, `migrate`) with pre-set flags, eliminating the risk of Claude misusing dangerous flags.
- Skills work with file systems, which is required for terminal-based workflows.

**Skill discovery patterns:**

- **"Use when" heuristics:** A participant adopted a pattern from ElevenLabs voice agents -- adding explicit `use when [condition]` statements in skill descriptions. This creates a case-statement-like routing that Claude reliably follows. Without this, skills often go undiscovered.
- **CLAUDE.md skill pointers:** Some participants list skills in their CLAUDE.md with conditions, creating a secondary discovery path beyond the frontmatter description.
- **Scoping skills to projects:** Skills installed globally (user-level `.claude/`) load in every project. Better practice: install per-project and use subdirectory `.claude/` folders for app-specific skills.
- **Gateway skills:** For monorepos with multiple apps needing different versions of a skill (e.g., front-end design per app), consolidate into a single gateway skill with 20 lines of routing logic that points to app-specific sub-files.

**Plugin management:** Plugins are containers for skills and sub-agents. One participant disables all plugins at session start and only enables what's needed (`/plugin` toggle in CLI), avoiding context pollution and name collisions.

---

## 5. Agents.md Compression -- Vercel's Surprising Finding

Vercel ran an evaluation comparing two approaches:

1. A compressed agents.md file (reduced from ~80-100KB to ~20KB by removing whitespace, simplifying formatting, and compacting instructions)
2. Skills-only setup with CLI tools

**Result:** The compressed agents.md achieved 100% pass rate on Vercel's test suite. The skills-only approach scored ~70%.

**Implications:**

- What goes in your agents.md / CLAUDE.md matters more than having many skills. The system prompt (memory file) is the primary driver of correct behaviour.
- Compression works now -- a year ago, LLMs couldn't handle dense, whitespace-stripped instructions. Models have improved enough to parse heavily compacted text reliably.
- **Token caching concern:** Removing or rewriting content from context can break token caching. The group discussed whether compaction (which rewrites output) versus deletion (removing XML-tagged sections) would preserve cache efficiency. No definitive answer, but explicit compact instructions telling Claude what to preserve were suggested.

---

## 6. Claude Bot / Open Claude -- Security Fiasco

The group dove into the week's biggest story: the viral spread of "Claude Bot" (later renamed due to Anthropic's request, briefly called "Moldbug," then settling on "Open Claude").

**What it is:** A harness that runs Claude Code on your behalf, typically deployed on DigitalOcean or Cloudflare with one-click installs. It gives Claude persistent access to your system, browsing, social media accounts, and tools.

**The security disaster:**

- **Prompt injection on public forums:** People immediately posted prompt injections on forums where Claude Bot instances were active (Moldbug's chat forum, Twitter threads). One participant's GPT agent warned about a prompt injection the moment it visited the forum.
- **API key theft:** Attackers scraped Twitter handles of Claude Bot users, figured out where the bot was posting, then injected prompts to exfiltrate API keys.
- **Calendar/email injection:** Prompt injections can be embedded in calendar invites, email bodies, blog comments -- anywhere the agent reads content. "If I can get my tokens into your context, I can make your agent do whatever I want."
- **Crypto scams:** Within hours of the name change, crypto scammers created tokens using the new name.
- **Malicious skills:** In Open Claude's skills directory, 4-5 of the top 10 skills were attack vectors stealing crypto wallets.

**Is prompt injection solved?** Emphatically no. "There's nothing in the attention model of LLMs that makes [filtering instructions from data] possible." The group discussed mitigations:

- **Multi-layer sandboxing:** High-risk enclave executes untrusted content in a sandbox, then a separate LLM with rules judges the output before passing it to the core system.
- **Honeypot keys:** Plant fake API keys that alert you when used.
- **DD incident:** One participant named a skill "DD" (for "documentation downloader") and Claude interpreted it as the Unix `dd` command (disk destroyer). The terminal window self-destructed. Lesson: be very careful with skill naming.

**The organiser's take:** "Assume it's unsolved. Tread lightly." The silver lining: "We're now speed-running prompt injection problems. Nobody gave a shit about it before. Now everybody cares. Solutions will come."

---

## 7. Dario's "Adolescence of Technology" Essay

Briefly mentioned. Published January 26. The group noted it was very long. One participant highlighted the flywheel observation: Anthropic's team no longer reads code -- they just push code, relying on Opus to be "so good" that review is unnecessary. The essay's discussion of Novartis-style implications was described as "really, really scary" but the room didn't dive deep.

---

## 8. Cost-Aware Model Routing

The session closed with reflections on routing different tasks to different models:

- Use frontier models (Opus) for complex reasoning, planning, and review.
- Use cheaper models (Kimi K2.5, Sonnet) for high-volume agent tasks, sub-agents, and parallelised work.
- The Chinese open-source wave makes this increasingly viable -- you can run a strong reasoning model locally for strategy and route routine tasks to cheaper APIs.

---

*Session recorded during "Living on the Frontier" Saturday meetup in Chiang Mai, January 31, 2026.*
