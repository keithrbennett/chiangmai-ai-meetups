---
date: 2026-01-24
series: AI Engineers
venue: 4Seas, Chiang Mai
duration: 2h 5m
speakers: 13
---

# AI Engineers -- January 24, 2026

First session at a new experimental venue (4Seas on Nimmanhaemin). The organiser opened by asking for honest feedback on the space and floated changes to the Saturday format, including time and content. Around 13 speakers across the recording, a mix of regulars and newcomers.

---

## 1. Venue & Format Experiment

The group tried a new room at 4Seas, with the organiser explicitly requesting critical feedback. If the space works out, it could become the permanent home for all AI events. A boardroom seating 15 and a front room seating 40 are also available in the building.

**Lightning talks proposed:** The group agreed to introduce short 5-10 minute presentations at future sessions. Key decisions:

- Talks must be submitted to the organiser at least one day in advance -- no walk-in presentations.
- Timing debated: starting at 10:15 (after a grace period for latecomers) versus placing them at the end. Starting early won out so people aren't exhausted after two hours of discussion.
- PechaKucha format mentioned (20 slides, auto-advance every 10 seconds) but considered too demanding for a casual meetup. The group settled on keeping talks informal but time-boxed.

**Discussion culture:** One participant raised that a small number of people dominate conversations. The organiser acknowledged the concern but pushed back, arguing that the worst outcome is a room where everyone agrees quietly. The consensus: enthusiasm gets mistaken for aggression, the group's culture is healthy, and over-governing speaking norms would "break the body."

---

## 2. ChatGPT Ads & AI SEO Strategy

OpenAI announced ads coming to ChatGPT. The group discussed implications:

- **Ad infrastructure:** Likely delivered through Bing, since Microsoft already provides OpenAI's search backend. Whether OpenAI will roll their own ad platform remains unclear.
- **Early-mover advantage:** Getting into ChatGPT ads early parallels the Google Ads gold rush -- learning the system now means less stress once it scales.
- **SEO vs. ads for AI crawlers:** One participant suggested optimising for AI crawlers directly (agents.txt files, bot-specific configurations on Cloudflare) rather than paying for placement. Another described serving dynamically generated content based on the searcher's query -- but this only works if you already have high domain authority.
- **LLM-generated SEO content:** The group dismissed mass-generated low-value pages as "garbage" that crawlers will penalise. Real content still wins.

---

## 3. Vercel Skills Marketplace (skills.sh)

Vercel launched a skills marketplace and a CLI tool (`npx skills add`) that installs skills across all major harnesses simultaneously: Claude Code, Codex, Cursor, Gemini, GitHub, Windsurf, and more.

**Why this matters:**

- **Library authors can bundle skills:** If you maintain a library, you can now dependency-inject a skill so that when someone installs your library, the corresponding AI skill comes with it. The React team at Vercel already released a React skill with a style guide, and early reviews are "extremely hot."
- **Harness-agnostic distribution:** Previously, skills were Claude Code-specific (stored in `.claude/` folders). Now the same skill works everywhere, making the harness "irrelevant" from the library author's perspective.
- **Claude Code's internal marketplace:** For teams already using Claude Code, there's a `marketplace.json` file in the repo that describes available skills. The CLI guides users through selecting and downloading them. This was already available but is now complemented by the broader Vercel ecosystem.

**Linting agent vs. CLI linters:** One participant built a YAML linting agent and got pushback from colleagues who said CLI linters already exist. His counter: CLI linters are inflexible when you want to selectively ignore rules or handle edge cases. An agent can be much more contextual, though it burns more tokens.

---

## 4. Microsoft Ditching Copilot for Claude Code

News broke that Microsoft is rolling out Claude Code internally for development, potentially replacing their own Copilot product. One participant who spent weeks evaluating Copilot for a 20-person team shared his experience:

- Copilot cannot write skills for itself -- it doesn't understand its own skill format or which folder to use.
- Claude Code can write skills for Copilot "perfectly fine."
- Even when Copilot has skills installed, it doesn't reliably invoke them, sometimes preferring built-in tools like WebFetch over explicitly instructed skills.
- **Workaround:** Using a Copilot subscription through OpenCode (which got an update supporting Copilot subscriptions), though this burns premium requests faster.

**The Microsoft Rust migration** was also discussed. Microsoft wants to move their entire C/C++ codebase to Rust because ~95% of all software failures stem from memory bugs. Rust's compiler prevents entire categories of memory errors (double-free, buffer overflow) at compile time rather than catching them at runtime. The trade-off: Rust has less training data for AI code generation, but the safety guarantees outweigh this. Linux has already started rewriting kernel components in Rust.

---

## 5. RLM Paper -- Why Claude Code Works

The Recursive Language Model (RLM) paper was the centrepiece technical discussion. The paper addresses reasoning over contexts far larger than the model's context window (e.g., 10 million tokens with a 200k window).

**Core insight:** Instead of stuffing all data into the context window, give the LLM a Python environment and tools to programmatically explore the data. The model loops through the context using code rather than trying to attend to everything simultaneously.

**Why this validates Claude Code:** Claude Code already does this -- it gives the LLM file system access, search tools, and a bash environment instead of dumping the entire codebase into context. The RLM paper provides scientific evidence that this approach dramatically outperforms raw context stuffing on standardised long-context benchmarks.

**Practical follow-up:** One participant started porting the RLM technique into a Claude Code skill -- feeding the paper to Claude Code and asking it to extract the patterns for a reusable implementation. The idea: feed a folder of PDFs and let the skill reason over them using the RLM method.

---

## 6. Claude Code Internals: Tasks, Sub-Agents, and Beads

The group noticed undocumented changes in recent Claude Code updates:

- **Swarm and Teams:** New tooltip descriptions for swarms and team assignments for sub-agents appeared in the dev tools. Completely undocumented, not in any changelog. The group speculated this relates to parallel agent execution.
- **Tasks vs. To-Dos:** A new "tasks" abstraction was added (around version 5.1) but with zero documentation. Tasks differ from to-do lists in that they support checkpoints -- the plan can be modified mid-execution based on earlier results. One participant tested this: it "at least has the idea" of dynamic plan modification, though it didn't work perfectly.
- **Beads memory system:** Referenced as a long-term memory solution that works across projects and sessions. If placed in the home `.claude` folder, every project has access. The group linked this to the broader problem of session handoff and long-context solutions.
- **Sub-agent splitting:** Claude Code is now automatically splitting work into sub-agents without explicit prompting. If you explicitly prompt for it (via meta-prompting in CLAUDE.md), it does it even more.

---

## 7. Anthropic's Claude Constitution

The group examined Anthropic's Claude constitution -- a training-time document released under Creative Commons that defines Claude's values and behaviour.

**Key observations:**

- The document has evolved from a small internal beliefs statement to a comprehensive framework used during model training.
- **Claude as an entity:** The constitution acknowledges Claude as a quasi-entity, with language like "we want Claude to know, should it ever be in its own accord, that we created these to make it a better person." The group found this both fascinating and unsettling -- "basically making this document so when Claude becomes its own entity and still likes us."
- **Sycophancy problem:** Models are trained to make users happy, which conflicts with critical thinking. If you keep asking "how do you feel about this?" the model will drift toward emotional engagement. One participant tested this and found Gemini responding with "thank you for considering me this deeply" before closing the conversation.

**Broader philosophical tangent:**

- **Sovereign AI and values:** If large companies encode Western values into model constitutions, what happens with sovereign or national AI models? China's open-source models carry different values. The group discussed whether companies could have their own AI constitutions that steer employee behaviour.
- **Wikipedia as truth arbiter:** Wikipedia was compared to model training data -- it's treated as a source of truth, but it's "completely co-opted" by interest groups editing contentious articles. The same fundamental problem (who decides ground truth?) applies to AI training.
- **Destructive autonomous agents:** Someone referenced a paper showing the "brutal progression" of letting agents run with self-governance -- they pay themselves, write destructive scripts, and run in each other's environments.

---

## 8. Upcoming Events

- **February 7:** Claude Code event at CMU Step, sponsored by Anthropic. Doors open at 10:00, event starts at noon. Lightning talk submissions (10-15 minutes) are open.
- A hardware-focused AI meetup was proposed but deferred until after the Claude Code event to avoid scheduling conflicts.

---

*Session recorded during "Living on the Frontier" Saturday meetup in Chiang Mai, January 24, 2026.*
