---
date: 2026-03-06
series: Agents in the Wild
venue: 4Seas, Chiang Mai
duration: 1h 20m
speakers: 10
---

# Agents in the Wild -- March 6, 2026

A Friday session with a large group covering code-generation workflows, the open-source agent tool explosion, AI skills security, and a market review of the OpenClaw ecosystem roughly 30 days after launch. The venue was 4Seas, confirmed by geo coordinates on the final segment.

---

## 1. AI Agents for Code Generation and Review

The opening conversation explored multi-agent code workflows:

- **Fresh-context review:** One participant argued that giving code to a completely new agent session for review reduces bias, because the original agent is inherently biased toward code it wrote. This mirrors the developer/QA split in traditional teams.
- **Codex-as-reviewer workflow:** A developer described using Codex to generate task prompts and review implementations, while Claude or other models write the actual code. Tests and diffs are the primary review artefacts.
- **CubLoop:** A recently released Ruby project -- an MCP server/CLI tool that sits between SimpleCov coverage JSON and an LLM. It helps create intelligent test-coverage strategies, supports CI gating based on Ruby-expressed predicates, and can orchestrate test augmentation across multiple agents. The author emphasised that test coverage is useful but easily gamed.
- **Front-end vs back-end quality:** AI-generated UI still requires many manual iterations and rarely reaches production quality. Back-end work feels more reliable with current tools.

---

## 2. AI as a Core Skill

The group debated whether AI fluency is becoming a fundamental skill on par with coding:

- People investing time now will pull away from those who are not, in the same way early coders gained lasting advantages.
- As interfaces get simpler (wrapped up by Claude, OpenAI, etc.), the cutting edge will always require deeper skills -- security hardening, custom tooling, and understanding the systems underneath.
- **Uncertainty about AGI:** If superintelligence arrives, current skills may become irrelevant. But the group's working assumption is that the current trend -- increasing returns to AI fluency -- holds for the foreseeable future.

---

## 3. AI Infrastructure and Tool Choices

A practical discussion about the state of the market:

- **No clear winner:** Every hosting and agent platform has tradeoffs. The group concluded that direct testing is currently necessary despite the pain.
- **Technical literacy matters:** Understanding how software and AI systems work under the hood provides durable value regardless of which specific tools win.
- **One-click hosted agents:** For non-technical users, hosted solutions (subscription-based AI agent services) are the pragmatic starting point. Examples include agents that auto-generate e-commerce product copy from simple instructions.
- **The learning-vs-waiting tradeoff:** Going through the pain of testing tools now means learning the space. Waiting for a clear winner means missing those learnings.

---

## 4. Open-Source Agent Tool Alternatives

A landscape review of OpenClaw-like open-source alternatives:

- **Projects surveyed:** Nanobot (already 30k GitHub stars at launch), Nano Claw, Pocket Paw, Hermes Aging, Pico Claw, Notis, Zero Claw.
- **Differentiation is minimal:** Most tools mirror each other in features. Some have a smaller footprint, but capabilities are nearly identical.
- **Historical parallel:** Before Cursor, there was an explosion of coding agent tools -- a new one every week. Months later, only Cursor, Claude Code, Codex, and Gemini survived. The same consolidation is likely coming to the agent-tool space.

---

## 5. AI Skills Security and Deployment

The group went deep on security implications of the emerging skills ecosystem:

- **Money flows:** Three areas attracting investment: distribution (one-click installs via DigitalOcean, Cloudflare), capabilities/skills marketplaces, and personas.
- **Review gaming:** Agent-generated five-star reviews can easily game skills marketplaces. Version skipping and breaking changes add further confusion.
- **Dependency injection attacks:** Skills are portable across harnesses, but if a skill references an NPM package that gets compromised, malicious code enters the chain. Classic supply-chain attack vector.
- **Hosting quirks:** DigitalOcean requires using Claude's API rather than the CLI due to "portable protection" restrictions.
- **OAuth and remote VMs:** One participant asked how to handle OAuth flows (e.g., Google Analytics, Search Console) when running via SSH on a headless VM. Solutions discussed: SSH port-forwarding the auth flow to a local browser, or avoiding interactive auth entirely by using tightly scoped service accounts.
- **Open gap:** Curated, auditable sandbox runtimes for skills do not yet exist. The group sees this as both a risk and a business opportunity.

---

## 6. OpenClaw Market Review -- 30 Days In

The session's closing presentation reviewed the OpenClaw ecosystem roughly one month after launch (January 26):

- **144 startups tracked** in the space -- unprecedented speed compared to the React ecosystem's early days.
- **$320k in publicly reported revenue** via TrustMirror/Stripe integrations, likely understating the real total significantly.
- **Personal agents as interface:** The presenter argued that personal AI agents will become the dominant way people interact with the world -- "you talk with your agent."
- **Weekly cadence:** The organiser reiterated that these events run every Friday and Saturday because the pace of change makes even a short absence hard to recover from. "Catching up is overwhelming."
- **Social:** After the formal session, the group mentioned heading to Moose rooftop bar, though attendance was uncertain.

---

*Session recorded during the Agents in the Wild Friday meetup in Chiang Mai, March 6, 2026.*
