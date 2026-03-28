---
date: 2025-10-04
series: AI Engineers
venue: 4Seas, Chiang Mai
---

# AI Engineers — October 4, 2025

## Developer Workflows: The "Surgeon vs. Tool-Caller" Strategy

- **GPT-5 (Codex): The Surgeon.** Extremely surgical and precise. Slower (15-30 minutes) but saves massive debugging time. Used in a "sterile" environment with no tools (MCPs).
- **Claude: The Tool-Caller & Prototyper.** Incredible speed and unmatched tool-calling ability. Excels at MCP interaction, filesystem modifications, running scripts. Less reliable for core coding.

## A Look at an Automated "Closed-Loop" System

A fully autonomous development agent named "Samantha":
- Uses a CLI wrapper to spin up a Docker container running Claude
- Given a virtual credit card and Namecheap account access
- Autonomously researched a topic, bought a domain, built a complete website with calculators and SEO-optimized blog posts, and deployed to Vercel — all overnight
- Strategy: give it a queue of 50 tasks overnight; the 2-3 successes represent massive productivity gains

## The Psychological Toll of AI-Powered Development

- Many members shared feelings of being constantly rushed (12-15 hour coding sprints followed by burnout)
- The Vicious Loop: fast prototyping → high expectations → cutting corners → technical debt → "Why did you build it wrong the first time?"
- Coping Strategy: aim to be fast (strategic advantage) but not feel rushed (detrimental internal state)

## The Future: AI as an Interface and the New SaaS Moat

- SaaS is evolving, not dying. The new primary moat is speed.
- MCPs and GraphQL: Use an existing GraphQL API as a "free" MCP server — LLMs can introspect a GraphQL schema and generate their own queries.
- OpenAI's "Agent-to-Commerce" protocol: conversational agents providing hyper-personalised recommendations instead of search/filter paradigms.
