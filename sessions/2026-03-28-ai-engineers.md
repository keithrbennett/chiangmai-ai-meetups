---
date: 2026-03-28
series: AI Engineers
session: 7
venue: The Kannas, Chiang Mai
duration: 2h 1m
speakers: 5
youtube: https://youtube.com/watch?v=N94ZBEvkjRk
transcript: ../transcripts/2026-03-28-ai-engineers.md
---

# AI Engineers — March 28, 2026

Saturday session with 5 participants. Smoky season in Chiang Mai has thinned attendance — the presenter noted that last year, all of March had near-empty sessions until the smoke cleared.

---

## 1. Guest Presentation: Rolling Out Claude Code in an Enterprise Team

Speaker 1 gave a 15-minute presentation on introducing Claude Code to a ~30-person team at a company with heavy regulatory requirements (ISO certifications, ISMS framework, full audit trails).

**The problem:** The company can't use Anthropic subscriptions directly. All model access goes through LiteLLM proxy to AWS Bedrock private instances, ensuring no data retention and no training on company data. This means Claude Code doesn't work out of the box — custom settings, environment variables, and API keys must be distributed to every user.

**The solution — a shared Git repo with:**

- **Automated onboarding:** Clone the repo, run a shell script (built with Ansible for idempotency), answer a few questions about API keys and MCP configs, and you're set up. Non-technical staff can use it without understanding JSON settings or folder structures.
- **Global CLAUDE.md:** A company-wide Claude MD file deployed to everyone's environment, providing sensible defaults and guiding toward more deterministic results across the team.
- **Shared plugins via marketplace:** Skills, agents, rules, and hooks are distributed as Claude Code plugins through a private marketplace JSON in the repo. Teams maintain their own plugins (MAP, DBR, DXP, PAI) while all plugins are visible to everyone — intentionally no permission gating so teams can learn from each other's experiments.
- **Shared knowledge base:** The biggest investment. Markdown files in Git organised by topic, each folder with its own CLAUDE.md for lazy loading (no context pollution). Three categories:
  1. **Issues & troubleshooting** — how to fix things, workarounds, diagnostics
  2. **External documentation** — local copies of vendor docs enriched with company context
  3. **Big picture knowledge** — org structure, who works on what, team responsibilities, infrastructure overview, scrum processes, Kubernetes platform details "down to the last detail"

**Why not a vector database?** No off-the-shelf solution supported collaboration, versioning, authentication, and permission control simultaneously. Cloud solutions were ruled out for data sovereignty. Markdown in Git turned out to be "a caveman method, but it works surprisingly well" — lazy-loaded via CLAUDE.md references, surprisingly token-efficient even with short descriptions.

**Reception:** 8 out of 10 positive. Team members were happy because they'd already struggled with settings.json and wanted to share knowledge beyond the built-in auto-memory (which is local and per-project only).

**Agent memory:** A separate concept — agents can persist their own memory between runs. Example: a weekly agent that scans the tech stack for updates and new tools, writes findings to the company Wiki, and keeps its own memory of what it reviewed last time for better diffs.

**Knowledge collaboration challenge:** Currently uses pull requests to master (only Speaker 1 can approve). The group discussed alternatives — Speaker 2 described an approach where an agent continuously rewrites/merges memory files rather than doing line-by-line diffs, which works well for solo use but scaling to 30 people is unresolved.

**Roadmap:**
1. Seed the knowledge base extensively ("unload everything that's in my head")
2. Better integration (e.g., `/update-ai-environment` command)
3. Fine-tune configuration and CLAUDE.md files
4. End-to-end workflows translating daily work into agent workflows
5. Full autonomy — assign a Jira story to Claude, it works and hands back for review

**Confluence migration:** The company still uses Confluence (required for audits/ISO compliance) but it's "terrible" with "the worst search I've ever seen." A git-change-reviewer agent diffs Jira stories against git changes against Wiki content, gradually shifting the source of truth from Confluence to Git.

---

## 2. Knowledge Management Debate

The presentation triggered an extended discussion on how to manage shared knowledge for agents:

- **ALS (Agent Language Specification)** was brought up again — its attribute-based access control could enforce who can write/read what, with YAML meta rules and compiler validation. Speaker 0 argued it could solve the permission problem without pull request gates.
- **Content validation vs. structural validation:** Speaker 1 raised the concern that structural checks don't catch wrong content or "poisoned" knowledge, which is also a security risk. The group acknowledged this as fundamentally hard — same problem exists with vector databases.
- **LLM hooks as reviewers:** The presenter suggested using Claude's LLM hooks (spawning a lightweight model like Haiku to review every write) to validate that sections contain required information and don't contain prohibited information. This mirrors how auto mode works.
- **Fine-tuning small models on domain knowledge:** Speaker 4 described training small models (LoRAs/SpineTunes) in 5-10 minutes on specific domain data, creating specialised models for search and retrieval rather than scanning thousands of markdown files. "For reads, go straight to the model. For writes, still use your source material."
- **ChromaDB's custom 20B model:** Speaker 2 mentioned ChromaDB's RAG system with a specialised model optimised for retrieval queries — you keep your data as markdown but let the model handle search, separating data storage from query intelligence.

---

## 3. Claude Desktop: Dispatch, Computer Control, and CoWork

**Dispatch (walkie-talkie mode):** Lets you interact with an active Claude Desktop session from your phone. Only syncs the one open session — it's not running anything new, just providing mobile access to whatever's running on your computer. Demonstrated live but was finicky.

**Computer control:** New feature requiring screen recording and accessibility permissions. In Anthropic's demo videos, it opens Excel and other apps. In practice during the meetup: didn't work at all. The group's verdict: "A hoax... classic Claude releases. The first two weeks, they just don't work." The presenter noted Anthropic is "so far ahead that they should consider slowing down."

**CoWork unlocked a use case for Speaker 0:** Previously, he'd work in Claude web, then manually copy-paste context into Claude Code. CoWork now shares the knowledge base between both, eliminating that friction. He can do ideation in the web UI and have Claude Code access the same context. "I finally figured out a use case for CoWork."

**CoWork vs. Claude Code:** Speaker 2 tested opening CoWork in a directory where he normally uses Claude Code — it behaved completely differently. Doesn't have the same skills, doesn't execute the same way. The group confirmed CoWork uses Claude Code under the hood but with a heavily modified system prompt.

---

## 4. Auto Mode (Teams Subscription Only)

New feature requiring a Teams subscription — not available on individual Max plans.

**How it works (per Speaker 2's research):** More sophisticated than simple permission-skipping. When Claude hits something requiring approval, it routes to a specialised model for quick triage. If that flags a concern, it escalates to a more thorough review agent that strips context and checks for prompt injection and other risks. "Quite a sophisticated system... definitely a step in the right direction."

**Comparison to existing approaches:** The presenter already maintains a large curated permission list manually. Auto mode should be smarter — particularly for dynamic bash code that Claude generates on the fly (Python for-loops, file processing scripts), which can't be pre-approved since they're different every time.

**The broader trend:** The group sees Claude moving toward generating throwaway code on the fly rather than invoking static CLI tools. Auto mode is the safety layer that makes this viable without requiring human review of every dynamic script.

---

## 5. Claude Code vs. Codex — Workflow Split (Revisited)

Strong consensus in the room on the workflow split, echoing last week:

- **Codex for coding:** "It trumps Opus by a lot. I don't use Claude for coding at all anymore." Codex "thinks really deeply about code changes" and is "extremely thorough."
- **Claude for planning and reviewing:** Better at review than Codex. But Opus 4.6 has two major complaints:
  1. **Trigger-happy:** Wants to start building immediately, even during brainstorming. "We're not even remotely close to thinking this through."
  2. **Walls of text:** Responds with huge outputs before jumping to action
- **Sonnet regression:** Speaker 1 felt Sonnet got "terribly dumb" after the 1M context window rollout — stuck in loops, trying the same failed approach five times.
- **Claude modifying code unsolicited:** Speaker 0 was building docs, Claude was reading the codebase to help, and it started updating the code because it noticed issues. "It has to reach consensus... all of a sudden, now you're ready to work."

**Cross-tool workflow:** Both Claude Code and Codex CLI support `/copy` commands for transferring context between sessions. Claude Code recently enhanced this — if there's a lot of output, it asks which part you want to copy.

---

## 6. Codex Plugins

OpenAI released plugins for Codex (video demo from the day before). Same concept as Claude Code plugins — containers for skills, agents, MCP configs, and rules distributed through a marketplace JSON.

Speaker 1 confirmed it works the same way as Claude's plugin system on the Codex CLI. One gap: he couldn't find how to add a custom marketplace (his own repo) to Codex, whereas Claude Code supports this natively.

**Plugin management in Claude Code:** The presenter demonstrated toggling plugins on/off in the CLI to manage context window usage — turning off unused plugins and running `reload plugins` to re-inject only what's needed for the current task.

---

## 7. Claude Code Auto-Fix

New feature: a toggle in Claude Code Desktop that, when connected to a GitHub repo, automatically attempts to fix CI failures. GitHub event triggers Claude to spawn, review the failure, and attempt a fix.

The group was cautiously interested but raised questions about customisation and control — how much you can configure what auto-fix does, and whether it's better to roll your own custom solution long-term.

---

## 8. Token Limits Tightening — Prediction Confirmed

The session ended on the news that Anthropic's Tariq announced adjustments to five-hour session limits during peak hours, with the claim that "total weekly usage remains the same" and only 7% of users are affected.

The group's reaction: "Total bullshit. If you go by the posts online, it seems to have affected everybody." This confirmed last week's prediction almost exactly — rather than raising prices, providers silently reduce allocation.

**The Thailand timezone problem:** An Anthropic employee encouraged US customers to shift workloads to off-peak hours, which directly overlaps with Thailand's working day. The presenter: "It's gonna encourage all these really smart people to fuck our shit over."

The session ran out of time before covering SPUD training and leaked model news.

---

*Session recorded during "Living on the Frontier" Saturday meetup in Chiang Mai, March 28, 2026.*
