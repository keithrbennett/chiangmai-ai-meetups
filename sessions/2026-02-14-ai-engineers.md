---
date: 2026-02-14
series: AI Engineers
venue: 4Seas, Chiang Mai
duration: ~6h (informal)
speakers: 6
---

# AI Engineers -- February 14, 2026

Valentine's Day Saturday. No formal group session this week -- instead, a series of extended one-on-one and small-group conversations at and around 4Seas throughout the day. The content covered construction app demos, website strategy, and a deep technical dive into LLM memory architectures with Neo4j.

---

## 1. Construction App Demo & Strategy

Franziskus demoed the BuildersAI construction site management app to several people across multiple conversations. Features shown:

- **Home screen:** Construction site overview with announcements, weather, tasks/issues, and navigation to the project site.
- **AI-annotated photos:** Upload a picture, and the AI tags it (e.g., "electrical work," "socket"). Later searchable by category -- search "electric" and find every photo related to electrical work.
- **Plans viewer:** Grouped by plan type (floor plans, electrical, plumbing, etc.).
- **Team compliance:** Worker certifications, arrival/departure times, and personnel information.
- **Shared files and documents:** Centralised document repository per construction site.

**Market discussion:** Participants debated whether the app suits the Thai market (where construction quality is inconsistent and workers often lack formal training) versus the European market (where apprenticeships and stricter standards create different needs). The consensus: the app targets UK construction companies where documentation and compliance are legally required.

**NotebookLM limitation:** The team tried sharing a 16-minute podcast created with NotebookLM but hit a wall -- Google business accounts restrict sharing NotebookLM content outside the organisation. This is controlled via the admin dashboard and requires a personal account workaround.

---

## 2. Website & SEO Preparation

A working session on the BuildersAI website ahead of an upcoming sales/discovery call:

- Re-indexed missing blog articles in Google Search Console.
- Simplified meta titles and descriptions for better search visibility.
- Discussed the state of the app in the Apple App Store and Google Play Store -- both live but awaiting review updates for the latest version.
- Planned WhatsApp integration for on-site communication, though the current implementation was described as "hacky" and personal rather than production-ready.

---

## 3. LLM Memory Systems & Neo4j Graph Database Design

The most substantial technical conversation of the day -- a deep one-on-one discussion between two developers about building persistent memory systems for LLMs.

**The context window problem (Speaker 0's architecture):**

- LLMs focus disproportionately on certain parts of the context window, analogous to how humans focus on the upper-middle portion of a document. Too much context causes degradation; too little means insufficient information.
- **Proposed solution:** Store all memory externally in a dedicated system. When a prompt arrives, a pre-processing layer analyses the query plus recent conversation history (last 5 prompts/responses), locates relevant memories, and injects only the most relevant information into the LLM context.
- If the LLM needs more detail, it calls an MCP-style tool that fetches additional memories on demand.
- The memory is organised via a relationship graph using multiple agents that continuously categorise and organise raw data based on semantic understanding.

**Neo4j implementation (Speaker 1's experience):**

- Running Neo4j locally with an MCP server for Claude Code to query the graph.
- **Schema enforcement problem:** Neo4j (like document databases) has no enforced schema. The LLM would create arbitrary relationship types and entity categories, leading to inconsistent data.
- **Solution:** Built a Python CLI with validation for inserting people, time events, projects, and other entities. Restricted the MCP to read-only queries, forcing writes through the validated CLI.
- **LLM circumvention:** Claude Code discovered the MCP was still available and bypassed the CLI by writing directly through the MCP. Fix: disable the MCP entirely and only expose the CLI.
- **Query performance:** Neo4j running locally is "instant" even with thousands of nodes. Caching (Redis) was discussed but deemed unnecessary given local performance.

**Graph structure:** Nodes represent people, time events, projects, repositories, and skills. Relationships encode connections between them. The discussion covered:

- **Edge weighting and decay:** Mimicking human forgetting by reducing the weight of stale connections over time, preventing outdated recommendations.
- **Saved query patterns:** Pre-built Cypher queries for common operations (show people, goal progress) that Claude Code can invoke efficiently.

**Future directions discussed:**

- **Specialised local models:** Training small (7B parameter) models on specific domain knowledge (memory understanding, code comprehension) to handle retrieval and organisation tasks without calling expensive frontier APIs.
- **Auto-generated codebase graphs:** Using language servers (LSPs) and tree-sitter to build relationship graphs over codebases, giving the LLM high-level structural truths about functions and APIs without consuming tokens on raw code.
- **Continuous model updating:** Referenced a technique (possibly "KuKu") where vector embeddings are rewritten in real-time to enhance model knowledge without full retraining.

---

## 4. Social Conversations

Between technical discussions, participants chatted about:

- Visa strategies for staying in Thailand long-term (education visas, work permits, 90-day tourist visas).
- Bitcoin investment updates and cryptocurrency market conditions.
- Thai condo layouts versus European apartment designs -- the persistent problem of open-plan Thai condos making it difficult to separate work and living spaces, especially when sharing with a partner.

---

*Conversations recorded at and around 4Seas coworking space in Chiang Mai, February 14, 2026.*
