---
date: 2026-03-21
series: AI Engineers
session: 6
venue: The Kannas, Chiang Mai
duration: 1h 57m
speakers: 6
youtube: https://youtube.com/watch?v=jRQChLlmjS0
transcript: ../transcripts/2026-03-21-ai-engineers.md
---

# AI Engineers — March 21, 2026

## Pre-session

Discussion about recording quality from previous sessions. The group is using 1,000-baht boundary mics — necessary because standard mics have noise cancellation that filters out room audio. Boya mics were out of stock locally and had to be rushed from Bangkok via Grab scooter (~200 baht). Plans to upgrade to XLR mics and a mixer if live stream viewership grows (currently ~3 viewers). Two more mics incoming (180 baht each). Ian offered to lend his existing audio gear.

The presenter explained his approach: minimal investment until there's consistent attendance. Yesterday's Friday session had about 3 in-person attendees. One participant noted he's more interested in transcripts than live streams.

Brief chat about smoky season in Chiang Mai, travel to China (Beijing, the Great Wall), and app ecosystems.

---

## 1. Claude Code Scheduled Tasks

Claude Code now has scheduled tasks in the desktop app — a feature Codex had from day one and CoWork had already introduced weeks prior. The `/loop` command (CLI only) is session-based and limited to three days, so it's a different thing.

**What's actually worth scheduling?**

Speaker 1 described a 45-minute automated workflow: scanning documents for issues, attempting fixes, running tests, and creating merge requests. Currently run manually, but with more generous token budgets he'd run it nightly. Another participant uses Codex automations for GitHub-based workflows — processing tables and reports.

The presenter noted he's been **moving away from GitHub entirely**, trying to avoid any infrastructure that isn't part of an agentic system — "it's just extra steps to get to it."

**The presenter's workflow split:**
- **Codex** for all coding — "it trumps Opus by a lot. I don't use Claude for coding at all anymore."
- **Claude** for planning, reviewing (considered superior at this), and personal agentic workflows — "Codex is terrible at that. Absolutely horrific."
- Scheduled automations follow the same split: Codex for code tasks, Claude for personal agentic tasks.

**Key insight:** The high-value scheduled tasks are **reflection-based** — analysis of what happened (daily summaries, standup reports from Slack, code health checks). Generative tasks that produce new content unsupervised ("wake up and 100 posts were done for me") were dismissed as "Jesus take the wheel" — too risky. Reflection skills can be tested once and trusted repeatedly; generative outputs are unpredictable.

Speaker 1 suggested the office use case: automated daily standup reports that summarise every Slack channel, ready for the team each morning.

---

## 2. Data Format Compression for Token Efficiency

A tangent on reducing token consumption through data format choices:

- **RX format** was mentioned — a JSON alternative that preserves semantics but restructures for compression. The group was sceptical: "It's gonna spend more tokens trying to figure out how to use the format." Benchmarks showed models don't understand alternative formats well, so you end up using more tokens in the long run.
- **Vercel's markdown compression** looked promising — they ran extensive benchmarks comparing normal markdown, agent MD files, and skill files through a compressor. Task completion accuracy was equal or higher post-compression, but all it did was reduce token count on load. "Nothing spectacular, but they did a whole bunch of tests on it."
- **CSV** was identified as the lowest-overhead format for tabular data (e.g., Reddit posts with title/description/username).
- **Parquet** was recommended for datasets with many repeated column values — "models use it for training data and are very good at using it."

Speaker 2 raised a more philosophical point about whether there should be a standardised open-source language for model communication that's language-agnostic — noting that open-source models are limited in their language support and coding-labelled models struggle with non-code topics. He mentioned having access to **EU AI supercomputers** in Slovakia with free compute for two months, inviting collaboration on research projects.

---

## 3. Token Pricing and the End of Unlimited Plans

**Off-peak discount:** Anthropic announced that until ~7 April, usage outside peak windows gets doubled allocation. The official off-peak window is weekends plus 5am–11am PT. For Thailand-based users, this covers roughly their entire working day (10am to late evening) plus all weekends.

**The $200 plan under threat:** An OpenAI executive stated on a podcast that unlimited token plans are unsustainable. Rumours suggest Anthropic will follow. Speaker 4: "There's nowhere to run to."

**The compute escalation problem:** The presenter laid out the core tension:
- Every new feature (sub-agents, batch processing, simplify commands) adds more compute time to tasks
- Previously: open CLI, say "add a feature", steer directly
- Now: 20 sub-agents build the feature → PR review with 10 sub-agents → simplify step → more sub-agents
- Result: token consumption has gone up dramatically, but so has output quality
- "How do you put all this into the calculus? You're saying you're using less, but I would argue you're not using the full power available to you."

**Historical context:**
- On a $100 plan, Opus previously gave ~20 minutes; now it gives a full 4-hour context window
- Context went from 200K to 1M at the same price
- One participant's friend runs a small company spending ~$20,000/month on AI tokens
- A $200 plan user likely costs the provider $1,000+ in actual compute

**Usage patterns in the room:**
- One participant uses it every day, many hours, typically hitting ~40% of weekly budget unless doing heavy text ingestion
- Another hits ~80% and wonders how to spend the rest
- Nobody was regularly exceeding their allocation

**The Uber/Lyft analogy:** Speaker 1 drew the parallel — artificially cheap pricing to build user base, inevitable price increases follow. "We're in the burning VC cash part of a new ecosystem. This will go away." When one provider raises prices, users swap to whoever still subsidises. "Burn the VC money while you can."

**Prediction from Speaker 2:** Rather than raising prices explicitly, providers will silently reduce allocation. "I don't think we're going to pay more. I think we're just going to get less."

**Counter-arguments:**
- Technology unit costs are deflationary — inference will get cheaper (Groq announcements suggest 10x)
- Context and model improvements mean more value per dollar over time
- Self-hosting on smaller models may become viable for non-frontier tasks
- China has already collapsed pricing ($200/year offerings)

---

## 4. Open Claw Token Burn and Agent Architecture

The group revisited why Open Claw users report burning millions of tokens after months of use:

1. **Poor structure** — agents searching through markdown files with inconsistent schemas, looking for content they can't find
2. **Caching failures** — early implementations didn't cache properly. Changing models mid-session, running garbage collection, or altering anything in the context window invalidates the cache, triggering full-cost recompute
3. **No structured entry points** — agents write directly to directories without validation

**Token burn as the new technical debt:** The presenter proposed that "how much token burn your system has due to fragmentation" is the new equivalent of technical debt.

Speaker 2 described his architecture: separating the personal agent system from structured coding agents. His personal agent delegates coding tasks to a dedicated CLI-based agent (with specialised skills and folder structure), which reports back when done. This keeps heavy token burn within the coding agent's budget, not the personal agent's.

---

## 5. Codex Sub-agents and CSV Batch Processing

Codex officially released sub-agents out of beta this week, with two notable features:

- **Recursive depth:** Unlike Claude Code (single level only), Codex sub-agents can spawn further sub-agents to configurable depth via an integer parameter
- **CSV batch processing (experimental):** Pass a CSV file where each row becomes a separate sub-agent task. "Codex reads the CSV, spawns one worker sub agent per row, and waits for the full batch to finish." Results are appended as a new column. Fire-once — no retry mechanism.

**Use cases discussed:**
- Processing lists of incidents, PRs, or migration targets
- E-commerce product enrichment (10,000 rows)
- Speaker 5 was excited about crypto back-testing with time series data

**Architecture debate:** Speaker 4 asked whether OpenAI should build queue infrastructure around this. The group leaned toward keeping it as a raw primitive — users can build their own queue/stream systems on top. Speaker 2 noted that "the moment you start numbering the process, it can't be a live queue" — better to let users control the abstraction. Speaker 0: "It's better that you control that rather than OpenAI makes it, because then we're stuck with whatever they give us."

---

## 6. GPT 5.4 Mini and Nano Models

OpenAI released mini and nano variants of GPT 5.4:

- **Speaker 5** upgraded from GPT 4.1 (which had been the only stable model for his project for a year) to 5.4 mini — load times dropped from 20–40 seconds to 8 seconds with cheaper costs
- **Mini:** Up to 400K context, $0.75/M input, $4.20/M output (corrected from earlier YouTube transcript figures)
- **Nano:** Even cheaper — less intelligent but suitable for simple classification
- Benchmarks show mini is surprisingly close to the full model, though the group was sceptical of self-generated benchmarks
- Speaker 1: "I'm not gonna use a mini model for software engineering. I'm gonna use it for text processing."

---

## 7. Jensen Huang's $250K Token Statement

At a two-hour Nvidia event and subsequent All-In podcast, Jensen Huang stated that if an engineer isn't using $250,000 worth of tokens, they're not a good fit. If they were only using $10,000, "he would be aghast."

**The group's interpretation:**
- It's about **leverage** — how many agents can you control simultaneously? How much productivity can one person extract?
- Token usage as a skill proxy: low usage = not leveraging AI; high usage = maximising available compute
- But it's imperfect: "Anyone can just run a loop of useless shit"
- **Critical nuance from Speaker 0:** Token burn correlates inversely with task novelty. Building classical, well-documented software (invoicing, CRUD) should consume massive tokens — LLMs excel there. Building on bleeding-edge tech with yesterday's documentation will have low token use because "LLMs are terrible at working on things on the frontier"

**Psychological impact of unlimited plans:** The freedom to experiment without cost anxiety accelerates skill development. Speaker 1: "If I'm limited, I'm gonna stop doing stupid stuff. I like doing stupid stuff now." Speaker 0: "The stupid stuff helps you learn what not to do, which makes you a better engineer than someone who doesn't know those pitfalls."

---

## 8. Auto-Research / Self-Improving Skills

Discussion of a pattern from a recent Karpathy interview and a YouTube video applying the auto-research paper to skill improvement:

- Originally about training models, but the pattern works for **iteratively improving prompts/skills**
- Three components: a harness (human-defined success criteria), automated test loops (~5 minutes each, up to 100 iterations), and comparison against previous iterations
- Each favourable result triggers a new test cycle; the system converges on an optimal solution
- Related to PlotCodes' SkillMaker, which has evals and auto-improvement "kind of built in, but not great"
- Speaker 5 was excited about applying this to crypto trading back-testing

**The presenter's approach to generating novel ideas:**
- Uses multiple harnesses (Claude Code + Codex) with the `/copy` command for handoffs between them
- Creates a deliberately rough first plan ("I know it's gonna be garbage"), then asks: "Now you know all this — recreate this plan from first principles"
- Does 2–3 iterations, picking the best ideas from each — "I don't want to think, I just want to grab"
- Speaker 1's technique: "Pre-prime an area of logic in the model and apply it against your plan. Tell the LLM to go find that idea, prime its context, then apply it against your plan."
- Both acknowledged this depends on the task — for truly novel/frontier work, human creativity still significantly outperforms LLM suggestions

---

## 9. Token Optimisation Strategies

A technical discussion on managing API costs:

- **Read-heavy workflows are cheap:** Input tokens cost far less than output. Spawn sub-agents that read many documents, summarise once, and return only the summary — highly cost-effective
- **System prompt caching:** Keep system prompts static with variable injection. The template stays cached; only injected variables change. Changing the model declaration (part of the system prompt) invalidates the cache and triggers full recompute
- **Why you can't switch models mid-session:** The harnesses (Claude Code, Codex) prevent or penalise model changes because it breaks caching. "They didn't want you changing the model 100 times in one session."
- **Batching:** For non-real-time workloads, batch API requests reduce costs significantly
- **Local caching:** One participant runs a cluster of 5–6 GPUs locally with models always held in memory — the cache never expires. This enables a self-improvement pipeline where classification results feed back into QA and labelling
- **Cache invalidation** remains one of the hard problems — the group discussed strategies for keeping caches warm and handling degradation

---

## 10. Rapid-fire: Other News This Week

In the final 8 minutes:

- **Dispatch from CoWork** — use your phone with CoWork
- **Claude Code Channels** — Telegram and Discord integration (covered in detail at Friday's session)
- **Remote control for Claude Code** — mobile access to CLI instances
- All three positioned as responses to the Open Claw phenomenon
- **Codex CLI now supports hooks** — post-tool-use validation
- **Generative interactive graphs** — deployable on websites, not just in-app
- **Claude Projects as CoWork** — projects created on claude.ai can now function as CoWork sessions
- **Cross-model access limitation** — when downgrading from the $200 Max plan to free, previous Opus conversation sessions became inaccessible to the free-tier model (Sonnet couldn't read them), though URLs could be made public as a workaround

---

*Session recorded during "Living on the Frontier" Saturday meetup in Chiang Mai, March 2026.*
