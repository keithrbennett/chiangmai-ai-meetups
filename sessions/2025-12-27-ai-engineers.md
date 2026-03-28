---
date: 2025-12-27
series: AI Engineers
venue: Chiang Mai
---

# AI Engineers — December 27, 2025

Holiday-season Saturday session. Quieter news week as Anthropic and most AI companies went on vacation. The discussion covered open-source model viability, harness comparisons, sub-agent workflows, context management strategies, and closed with a wide-ranging conversation about using AI for organisational management and compressing business feedback loops.

---

## 1. Open-Source Models and Local Hardware Limits

GLM 4.7 released on December 22. Speaker 1 tested it in Claude Code (switching the backend) but struggled — the model lacks the post-training that makes tool calling work reliably in harnesses like Claude Code. "It can't use the tool that is in Claude Code... the plan tool."

The group's consensus on large open-source models: running a 700B parameter model locally requires clustering hardware and still only yields ~15 tokens per second. Speaker 3 confirmed that even 120B models need two 96GB cards, putting you "in $20k territory." At 200k context, performance degrades further: "It's slow as shit."

**The alternative — small, purpose-built models:** Speaker 1 argued the path forward is smaller fine-tuned models (3B-30B parameters) acting as specialised nodes in a network. Rather than one massive general-purpose model running locally, use highly precise small models triggered for specific scenarios. A 300M embedding model running through MX in a container was "very, very lightweight, and it does the job perfectly."

**Hybrid local-API pattern:** Speaker 3 described OpenAI's demo approach — give a small open-source model a tool to call GPT-4 when its confidence is low. Process sensitive PDFs locally, ship everything else to the API. "The small models are pretty dumb, but when you tell them to go out and fetch context, they can do whatever you would want to do."

---

## 2. Post-Training as the Secret Sauce

The group discussed why Claude feels so much smarter than raw model benchmarks suggest. Speaker 0's theory: Anthropic has identified which tools the model should consistently call and in what direction it should build projects, then bakes that into post-training. "It makes the model look really, really smart until you just do something really esoteric, and then you start to see Sonnet 3.5 show up."

Speaker 4 extended the point — the skills may not actually be generalised. They come from training on great examples in popular languages. Switch to an obscure language and the model hasn't "actually generalized the skill of making a plan across different languages."

Speaker 0 referenced a podcast (from ~2 weeks prior) comparing current model training to coding competition specialists: excellent at competition problems, useless in business scenarios. The saving grace is that Anthropic's post-training targets business use cases.

---

## 3. OpenCode and AutoClod — New Harnesses

**OpenCode** is gaining traction as an alternative CLI harness. Key features discussed:

- Supports 12 different model backends using ACP protocol to communicate with each provider's native CLI
- Had LSP integration long before Claude Code (which added it as a plugin that same week)
- Includes heuristics for determining whether shell commands are safe, with colour-coded risk indicators
- Speaker 7: "It uses the original ones that the models are trained for, but they use the ACP protocol to communicate with the other harness. You get a unified interface with the file browser."

**AutoClod** — a newer tool that drew strong interest:

- Provides a Kanban board interface, memory system, Git issue queue integration
- Uses a graph database backend (recently switched from file-based to LadybugDB)
- Includes different agent profiles (testing agent, PM agent, QA agent) similar to BMAD methodology
- Speaker 3: "It has different agents that will do stuff like testing agent, project manager agent, QA... if you give it a task, it'll run through the loop on the different agent profiles."
- Very active development — "eight releases a day" on a repo with nearly 4,000 stars and 480 forks
- Group advice: "Maybe wait. But it looks really cool."

---

## 4. Multi-Terminal Agent Workflows

Speaker 0 polled the room: most participants run at least two terminal panes with harness instances; some run three or more.

**Speaker 10's BMAD workflow:** One terminal per user story, not per agent. The workflow sequences through intake, scrum master, developer, and QA agents within a single conversation to preserve context. Agents hand off via conversation text rather than files ("I don't want pollution of data"). Each agent has instructions for how to communicate with the others. "If I'm context engineering, a window is a story, and everyone gets their turn, and then I delete the conversation."

**Sub-agent quality concern:** Speaker 10 found background sub-agents unreliable for complex tasks: "They go off under the water and do all this crap, and they come back and say, we're done. I go, what have you done? I don't know. Did it work? And nine times out of ten, it didn't work."

Speaker 2 suggested the principle: "One terminal, one primary agent." Sub-agents help with discrete tasks, but you need visibility and control at the top level.

---

## 5. Context Management — Abridgement vs. Compact

Speaker 10 raised the difference between abridgement and Claude Code's compact command. Claude confirmed to him that "compact does not work like an abridgement — it's really just trying compression."

Speaker 3's recommended pattern: do your abridgement, but link back to the original full-length document. "One of the hardest things is trying to do compaction of context... the best method was compact or do whatever you need to do to get something that fits, but also have it in length. Sometimes you'll pull up because you'll see it in the abridgement — it can grab and get the full context."

Speaker 4 raised a deeper concern about custom data formats: "There's no way to benchmark that Claude is actually taking on that format internally." Needle-in-haystack recall tests don't prove the model understands a custom format. You may need 10,000 tokens of context explaining how to use the format, at which point the gains from compression are diminishing.

---

## 6. Sub-Agents — Deterministic vs. Fuzzy Use Cases

**Speaker 9's morning report system:** Spins up eight sub-agents simultaneously to pull data from different sources (Google Calendar, etc.), passes results to an orchestrator, which routes to an analysis sub-agent, then to a Notion document creator. Each sub-agent has exactly one tool and one task. "Out of the thousands of times I've run each agent, I've never had it screw up."

Speaker 4 challenged this: "If it's that deterministic, why not just have a Python script?" Speaker 9's response: it's about flexible composition — not every run needs the same data, and the orchestrator can route dynamically.

**Speaker 3's documentation downloader:** A sub-agent skill that fetches documentation, tries to find markdown on GitHub first, fuzzy-matches against the original web page, and falls back to HTML-to-markdown conversion. "There's a little bit of fuzzy logic for me." The key benefit: the sub-agent handles fetching without polluting the main agent's context window.

**Speaker 0's fan-out pattern:** Spin up five explorer sub-agents to search for the same thing from different angles (budget perspective, critical perspective, etc.), then judge all five outputs. "My biggest change is that I've become very comfortable trusting Opus to write prompts for me to give to sub agents." He observed that the general-purpose sub-agent behaves identically to the primary agent, which means mastering the primary agent's behaviour directly transfers to predicting sub-agent output.

**Pre-prompt processing concept:** Speaker 0 described a mental test — write your prompt on paper before typing it. If you can predict what the model will return and you're 90% right, "your intimacy with the model is really strong." That intimacy is what makes delegation to sub-agents reliable.

---

## 7. Swarms — Still Theoretical

The group discussed swarm architectures. Speaker 10: "We won't see swarms until background agents can talk to each other." Speaker 3 speculated that the auto-compaction memory system could serve as a message bus between agents — agents writing memory that other agents can read.

Speaker 0 referenced Anthropic's Daisy, who reportedly built the Claude Code plugin system over a weekend using some swarm-like workflow, but the details remain unknown. "Everyone's got a different idea of what swarm is, which already confuses me."

Speaker 3 cited the OpenAI deep research team's conclusion: "Swarms don't work... you can't do it asynchronously. You have to wait till everything finishes, read all the context, and do something on it."

---

## 8. Claude Code as a Life Tool — Beyond Coding

A newcomer (Speaker 5, currently on Cursor) asked whether people use Claude Code for non-coding tasks. The overwhelming answer: yes.

Speaker 3's pitch: "We call it Claude Code, but all we're really talking about is the terminal... you can ask it any bullshit you want." The file system advantage is the killer feature — Claude Code writes artefacts to disk, so you build up a queryable local knowledge base over time rather than copy-pasting from web interfaces.

Speaker 9: "My entire life lives in Claude Code. Health, everything is all in the system."

**The system prompt caveat:** Speaker 6 recommended reading Claude Code's system prompt (extractable by asking it to explain its tools, then write them to the file system). The system prompt is heavily optimised for programming — Git history, logs, code-oriented directives. For non-code tasks like fitness or relationships, the programming framing can bias outputs toward "the hybrid approach" averaging. Speaker 6's advice: "Think from first principles — this is a model, there's a system prompt, there's access to certain tools. What combination of all these atomic units makes sense to achieve the output of that task?"

Speaker 1 noted you can override the system prompt using a container environment, though Speaker 6 clarified you can override but not fully rewrite the baked-in CLI system prompt.

---

## 9. Competitive Intelligence Automation

Speaker 3 described building automated competitive analysis pipelines: scripts that take a website and competitors as input, then run for two hours pulling Google Ads transparency data, UK company registry information (director names, other businesses, bankruptcy filings), and web content. "I didn't program any of this in. It just kinda does it. Like, 'these guys are going bankrupt' or 'their founder just died — you should really attack.'"

The system predates formal agent tooling — built from chained markdown prompt files that run in parallel, with deterministic code replacing steps that failed repeatedly. Output includes SWOT analysis and competitive reports. Early versions hallucinated heavily; grounding in citations and manual verification solved this.

---

## 10. AI for Organisational Management and Business Feedback Loops

Speaker 5 raised the question of using AI to improve information flow in organisations — syncing leadership context with team members, preserving institutional knowledge when people leave.

**Speaker 1's approach:** Use a knowledge graph (Neo4j) via MCP. New hires interact with an AI that has company context (projects, vision, mission). The AI ensures their proposals align with organisational direction. Output goes to an interim memory store; a curator filters key learnings into a shared knowledge base.

**Speaker 6's first-principles challenge:** Traditional organisational structures (departments, SOPs, knowledge transfer) exist because of time constraints. As AI compresses learning time, these structures may become unnecessary. "When Opus 4.5 came out, I literally deleted half of my code base because it wasn't relevant anymore." The question becomes: can agents learn just-in-time rather than through pre-compiled organisational knowledge?

**Compressing business feedback loops:** Speaker 6 described the pattern — launch an offer instantly (AI generates creatives in seconds), run ads, measure response, iterate. What used to take weeks now takes hours. Speaker 2 extended this: hook automations into the feedback so the product itself changes based on real-time response data.

Speaker 4 connected this to how AI providers game benchmarks: "They tried it 500 times and then got the answer. Isn't that just [the same pattern]?"

---

*Session recorded during "AI Engineers" Saturday meetup in Chiang Mai, December 27, 2025.*
