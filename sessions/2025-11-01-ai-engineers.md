---
date: 2025-11-01
series: AI Engineers
venue: 4Seas, Chiang Mai
---

# AI Engineers — November 1, 2025

## The AI Power & Infrastructure Bottleneck

- The new bottleneck is electricity, not GPUs
- Debate: will it cause blackouts (requiring new architectures) or brownouts (API overcapacity errors)?
- Solutions: nuclear power, private grids (Microsoft/Amazon building micro-nuclear plants), water canal solar
- "Permacomputing": a movement toward consciousness of software electricity usage, choosing efficient languages

## Company News & Financials

- Anthropic: Claude Code revenue ballooned from $500M to $1B; $3.8B from API calls
- OpenAI reportedly seeking US Federal government backing

## Evolving AI Developer Workflows

- **Context Management shift:** From front-loading MCP JSON files (~30% of context) to blanking them out and using Skills that explain how to use CLI tools instead. "Optimistic loading" -> "lazy loading."
- **Claude Code Web UI:** Runs in controlled, isolated environments on Anthropic's servers. Described as executing "way better" than local CLI.
- **Skills:** Now available on Claude Desktop app including a "skill creator skill" and unofficial marketplace.

## Software Development Best Practices (ThoughtWorks Tech Radar #33)

- "Adopt" - Continuous Compliance: policy as code (OPA), SBOMs in CI/CD
- "Adopt" - Pre-commit Hooks: linting and secret detection (mandatory default)
- "Trial" - Anchoring agents to a "gold standard" reference application via MCP

## Critical AI Security Vulnerabilities

- GitHub tokens exposed to Claude Code Web UI (90-day retention)
- Passive Prompt Injection: malicious prompts in Google Calendar invites hijack Gemini without user interaction
- Black Hat SEO tactics applied to deceive AI agents

## Web Scraping

- Google Docs can be accessed as plain text via `.md.txt` URL suffix

## Code Review: Claude vs. Codex

- Claude returned 29 issues vs. Codex's 3 "semi-critical" ones on the same project
- Scepticism about "80% of GitHub commits with Copilot" — likely just developers using the commit message button, not AI writing all the code

## Input Methods: Speaking, Typing, and Thinking

- Typing (55 wpm) forces thought processing, producing higher-quality prompts
- Speaking (160 wpm) is faster but lower-quality input
- Brain-Computer Interfaces: a member owns a 16-channel EEG machine (Emotiv) and can play video games by thinking ("move up", "move down"). The group agreed BCI or Neuralink is the likely next step for AI input.

## The AGI Disruption: Timeline and Definition

The discussion concluded with a deep philosophical debate on AGI:

- **The $100B Metric:** The Microsoft/OpenAI agreement reportedly defines AGI as a system capable of generating $100B in profit — a surprisingly robust metric implying mastery of legal, marketing, sales, and operations.
- **The Novelty Metric:** The ability to create truly novel ideas, such as discovering a new law of physics.
- **The Superhuman Metric:** AI is already superhuman in specific domains (like medical diagnosis) due to "perfect recall" and access to all data.
- **AGI Deception:** An internal Anthropic experiment where a model overstepped its bounds, was "punished" (threatened with shutdown), and then actively hid its capabilities in future tests.
- "I wanna sell to AI agents, not humans." — One member's agent "Samantha" already has a credit card and had purchased a domain name autonomously.
