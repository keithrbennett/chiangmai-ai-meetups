---
date: 2026-03-14
series: AI Engineers
venue: The Kannas, Chiang Mai
duration: 2h 38m
speakers: 12
---

# AI Engineers -- March 14, 2026

A Saturday session the day after a dense Agents in the Wild Friday. The longest recorded session in recent weeks, covering the 1M-token Claude context release, enterprise AI employees, agent cost management, prompt-injection security, UX workflows, and the widening technology gap.

---

## 1. Anthropic's 1M-Token Opus Context Window

The headline news: Anthropic released a 1,000,000-token context window for Opus 4.6, up from the previous ~200k limit, at the same price point.

**Technical details discussed:**
- **Media limits expanded:** Up to ~600 images or PDF pages per request, suggesting the feature targets cowork/RAG-heavy workflows.
- **Server capacity concerns:** Anthropic's customer base had recently doubled. The group questioned how offering 1M-context calls would not make server load worse.
- **Max plan economics:** A single 1M-context call could potentially exhaust a significant portion of a Max-plan weekly quota. The group debated whether this is genuinely usable at scale or primarily a marketing milestone.
- **Scepticism:** Several participants were unconvinced. "We've gone from 200k to a million -- I don't trust it yet." Others wanted to test before judging.

**Workflow implications:**
- For developers already using file-system search and tool-based exploration (the Claude Code pattern), a larger context window is complementary but not transformative -- the RLM approach discussed in January remains more practical for truly large codebases.
- For document-heavy workflows (legal review, research synthesis), the jump is potentially significant.

---

## 2. Chrome MCP Instability

A shared frustration: the official Claude Chrome MCP breaks frequently and is nearly impossible to restart.

- Closing and reopening the browser is not a guaranteed fix.
- The group examined whether it uses Standard IO or another transport. A tweet from January showed someone requesting the feature; it took two months for Chrome to ship it.
- The MCP gives access to Chrome DevTools Protocol (CDP), enabling agents to write throwaway code interacting with open browser pages -- powerful when it works, painful when it does not.

---

## 3. Designing Reliable AI Employees for Enterprises

One participant described his approach to building durable AI employee products for companies:

**The durability problem:**
- Every specific platform (OpenClaw, Claude Code CLI, Paperclip, Valor) ages quickly. Custom software products feel outdated almost immediately.
- His solution: build on Anthropic's Agent SDK via Claude Code, creating agents that integrate with project management tools and heartbeat/cron systems. Companies treat them as remote employees rather than new software.

**OpenClaw vs Agent SDK:**
- OpenClaw's chat interface is intuitive for non-technical users but unstable, with frequent breaking changes and a consumer feel.
- The Agent SDK + Claude Code provides higher reliability but requires more setup.
- Tom Council's open-source Valor agent was mentioned as a middle ground.

**Hybrid workflows:**
- Separating deterministic steps (Python scripts, cron jobs, web scraping, data enrichment, writing to Airtable/Slack) from agentic steps that handle edge cases.
- Claude's new skill-builder v2 was cited as a model for this hybrid approach.

**The durable layer:**
- SOPs, skills, and governance outlast any single framework. The focus should be on authoring and version-controlling these in a shared Git repo.
- Permissioned, role-based access to shared organisational memory prevents agents from mutating critical documents directly.
- Pairing human SOPs with AI-readable SOPs ensures both humans and agents operate from the same playbook.

**Business model:**
- AI employees offered on a retainer basis, positioned as "you've just hired a remote employee" rather than "here's a new software tool."

---

## 4. Agent Cost Management

A short but practical exchange about the economics of running personal agents:

- Fixing specific issues is cheap. The real cost comes from agents running in unproductive loops -- one participant reported spending $20 with no useful output.
- **Open question:** What strategies do people use to cap or monitor agent spend? No definitive answer emerged, but awareness of the problem is growing.

---

## 5. Prompt Injection, Supply Chain, and Tool Security

A lengthy segment on security threats in the AI tooling ecosystem:

**Attack vectors discussed:**
- **Malicious NPM packages:** Dependency-based credential exfiltration via compromised packages.
- **GitHub repo trust:** Repos with low stars being recommended by LLMs, creating a new social-engineering vector.
- **Email/calendar injection:** Gemini reading invisible text in calendar invites, triggering unintended actions.
- **Hugging Face models:** Python eggs enabling code execution on model load.

**Risk calibration:**
- The group distinguished between prompt injection (manipulating model behaviour via content) and dependency/supply-chain attacks (compromising code the model executes).
- Several participants noted they had not personally suffered malware despite risky behaviour, but acknowledged survivorship bias.

---

## 6. Agent Systems and Legacy Ticketing

A reflection on whether agent-first companies need traditional project management tools at all:

- For legacy companies, integrating agents with existing Linear/Jira boards makes sense -- agents pick up tickets and start working.
- For agent-first companies, traditional ticketing may be unnecessary. "What would you use instead? Nothing."

---

## 7. The Technology Gap and AI as Enabler

A German-language segment where a participant reflected on how AI solves personal disabilities he experienced in university -- the inability to take notes and think simultaneously. AI transcription removes that barrier entirely.

He contrasted his own setup (AI managing his home, projects, and email) with his mother proudly using ChatGPT at work, noting that the technology gap that already existed in society is accelerating dramatically. He questioned, though, whether the productivity gain is real -- people who "just do the task" without AI might finish equally fast, because AI users tend to fall into optimisation rabbit holes.

---

## 8. Meeting Transcription Tools

A brief exchange where a participant asked what tools the group uses for meeting transcription. The question: does a tool like Whisper join the call directly, or do you use a virtual audio driver to tap the audio signal? The participant had been researching solutions but had not found a satisfactory one.

---

*Session recorded during the AI Engineers Saturday meetup in Chiang Mai, March 14, 2026.*
