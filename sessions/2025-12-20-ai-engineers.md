---
date: 2025-12-20
series: AI Engineers
venue: CMU, Chiang Mai
---

# AI Engineers — December 20, 2025

Claude Code community event in Chiang Mai with multiple presentations and networking. Anthropic-sponsored, with a raffle for a Max subscription. The organisers mentioned planning monthly events going forward and a hackathon, noting that "Anthropic wants to invest a lot into the community here in Chiang Mai." Three talks covered building SaaS with Claude Code, sleep-time agent memory systems, and async sub-agents.

---

## 1. Building and Selling SaaS with Claude Code — Johan Svenathan

Johan (Speaker 0) presented on using Claude Code to build, optimise, and sell SaaS businesses. He runs three SaaS products simultaneously through his company Jarvis Global, something he said would have been impossible five years ago without hiring developers.

**Funnel analysis with PostHog MCP:** Johan described having Claude Code analyse his codebase, understand the customer journey, and auto-generate PostHog funnels. His example was a Twitter outreach tool where users must connect their account, scrape leads, then start cold outreach campaigns. "I thought it was those four steps. When I looked at the funnel that PostHog made, it was like 10 other steps." The deeper funnel exposed that users were dropping off at account connection — the critical first step.

**Iterative optimisation loop:** Collect funnel data for 10-15 days, then have Claude Code analyse drop-off points and brainstorm improvements. For his account connection problem: optimise the UI, simplify the flow, and — when the product itself can only go so far — add lifecycle emails. "People who aren't connecting their accounts, there's only so much we can really do. We can optimise the UI... but if people don't really understand it, we send them an email after 24 hours with a video."

**Onboarding emails as a revenue lever:** Johan stressed that onboarding and lifecycle emails were where he "left money on the table" when selling his first business. The strategy: keep emailing users "until they buy or die or unsubscribe" to guide them through the funnel.

**Automating the business, not just the code:** Claude Code handles auto-generated documentation, SOPs, and customer support workflows — not just software development. The goal is making the business owner-independent: "You wanna be able to go to a buyer and say, look, I have this business that can run entirely without me." He sold his previous product after two months of not touching it, which was "very incentivising for the buyer." His model: "calm, profitable, sellable anytime."

---

## 2. Kybernesis: Sleep-Time Agents and Semantic Tool Selection

Ian (Speaker 2) and Daniel (Speaker 5) presented Kybernesis, a three-layer system consisting of a memory layer, an agent layer, and an action layer. The core innovation is replacing RAG with sleep-time agents.

**Sleep-time vs. task-time retrieval:** Traditional RAG is task-time — when you need information, an agent searches, processes, and returns it, consuming significant tokens and time. Kybernesis runs an agent in the background 24/7 that "actually knows the answer before you ask it." The result: what would normally cost 30,000 tokens for a RAG request gets reduced to under 800 tokens, because "everything has been thought of and answered and processed ahead of time, building relationships and stuff." The concept comes from a university research paper from the prior year.

**Semantic tool selection:** Daniel demonstrated the problem with large MCP servers — GitHub's MCP has ~93 tools, and every query sends all tool definitions to the LLM, quickly bloating context. Their solution decomposes tools into a Neo4j graph or vector store, creating embeddings for parameters and return types as well as tool descriptions. At query time, only semantically relevant tools are sent to the LLM.

**Live demo results:** A single message with all 93 GitHub tools used ~20,000 tokens. With vector search enabled and only relevant tools selected, the same query dropped to roughly 4,000 tokens. "If you do it with just one message, you may not see the results. But if you have 10 messages or more, then you're really gonna start to see these results."

**SDK integration:** For developers using the AI SDK, they offer a drop-in plugin — call a sync method and "your application will be kind of like RAG proof."

**Beyond tools — conversation memory:** The same graph-based approach extends to conversation history, agent relationships, and swarm coordination. Everything gets processed in the background by Kybernesis and stored in a memory layer, taking the concept "a step higher with everything in your agent stored in some form of memory layer."

---

## 3. Async Sub-Agents and the Captain's Chair — Nick

Nick (Speaker 4) focused on Claude Code's recently released asynchronous sub-agent capabilities, which he'd been stress-testing all week.

**Sub-agent basics:** Claude Code (the "harness" or primary agent) can spawn instances of itself to perform specific tasks. Two weeks prior, sub-agents blocked the UI — you had to wait for them to finish. The new async mode lets sub-agents run in the background while you continue working in the main session.

**Five native sub-agents in Claude Code:**
1. **Plan mode** — recently migrated to be a sub-agent, spawns with its own system prompt and context window, writes a plan to a file
2. **Explore** — a quick Haiku-based agent for exploration
3. **General purpose agent** — used when you explicitly ask Claude to spawn a sub-agent, defaults to Sonnet (can be overridden to Opus)
4. **Claude Code Guide** — documentation lookups about Claude Code itself
5. **Status Line** — the most recent addition, not yet listed in the official docs

**Key technical details:**
- Sub-agents are token-bound, not time-bound. Nick tested by falling asleep with agents running and woke to find they'd been alive over 24 hours.
- Background processes persist after an agent terminates — if a sub-agent starts a dev server, that server keeps running even if the agent dies.
- Permission inheritance is a major gotcha: sub-agents inherit permissions from the harness. If you click "allow once" instead of "always allow," sub-agents silently fail without useful error messages. "It took a lot of digging for me to figure out that there's a permission inheritance structure."
- Spawning many sub-agents simultaneously works — Nick saw people on Twitter running ~80 background sub-agents. His own tests ran five simultaneously without issues.

**Live demo — the "Captain's Chair" concept:** Nick spawned four async sub-agents (WhatsApp monitor, ads manager, email monitor, meeting assistant) connected to mock servers, plus four dev servers with Chrome MCP integration. Without touching the keyboard:
- A WhatsApp sub-agent surfaced a message from "Sarah, wife of golf buddy Mike Chen" and asked if he wanted to handle it. He said "handle later" and Claude respawned the agent to monitor for the next message.
- An email sub-agent flagged a security alert about unusual database access patterns, recognising it as important enough to escalate rather than handling autonomously.
- A meeting sub-agent notified him of an upcoming board meeting.
- Meanwhile, three additional sub-agents were spawned to develop a dark mode feature on one of the websites — the feature was completed while Nick was talking and handling other agent notifications.

The terminal showed seven background shell tasks and multiple async agents running simultaneously. Nick described the concept as "the captain's chair — you sit in front of one Claude Code session, no more like eight Cloud windows opened up next to each other in your terminal."

**Chrome MCP:** Anthropic's new native Chrome MCP connector (in beta) was demonstrated — Claude opened browsers, navigated websites, took screenshots, and made decisions based on what it saw. The toolset includes recording capabilities useful for testing.

**Other new features mentioned but not demoed due to time:** Ralph Wiggum agentic strategy (from the official Anthropic marketplace — reportedly used to "complete a $50,000 contract using only $297 in API credits"), and a new alternative to spec-driven development.

---

## 4. Networking: Construction Tech, AI for Small Business, and the Engineer-Sales Gap

Extended conversations after the talks covered several threads:

**Graph databases for personal and business knowledge:** One participant (Speaker 3 / Franziskus) discussed feeding chat conversations, WhatsApp messages, and other contextual data into graph databases to build structured knowledge with relationships — people, businesses, skill sets. "There's already so much documentation that can be derived from all these contexts."

**Construction AI use cases:** A lengthy conversation between Franziskus (building a UK construction SaaS) and Richard (Speaker 1, American with construction and restaurant background) explored practical applications:
- **Communication as the killer feature:** "Communications is the key thing. Changes in schedule, delays in materials... when you're halfway through a job and someone's driven a forklift through all your fucking windows." The AI could present scenarios: "Windows are delayed two weeks. We have this option, this option, and this option."
- **Voice recording for documentation:** Richard strongly advocated for recording site conversations and phone calls — "a lot of the problems that you run into with subcontractors or clients is a lot of it's fucking verbal. Doesn't get written down." Both parties would benefit from records of commitments and change approvals.
- **Compliance and regulation as the easy sell:** Richard shared examples from running restaurants — a chef sued for not receiving mandated breaks, resulting in a $3M fine. "Compliance and regulation is an easy sell. Even more so than productivity and efficiency." He noted that as a business owner, he "spent most of my time concerned about stuff like sexual harassment, timekeeping, safety training, insurance."
- **Environmental regulations:** Erosion barriers for soil runoff during excavation, dust control fencing in dry areas — all checkable against task schedules and weather forecasts.
- **Small business focus:** "A hundred times, if you help out that small business person, the sale will be very easy. Because they need all the help they can get." Small builders can't afford dedicated HR, legal, or compliance staff but face the same regulatory exposure.
- **Offline capability matters:** Construction sites often lack reliable connectivity, especially in concrete structures or basements. The app's local-first database with cloud sync was discussed as important.

**The engineer-sales gap:** Multiple participants noted Chiang Mai has a large pool of engineers but lacks business and marketing people. "There are so many good products, we're building good products, but the shitty products make money because they have good marketing and good sales."

---

*Session recorded at a Claude Code community event in Chiang Mai, December 20, 2025.*
