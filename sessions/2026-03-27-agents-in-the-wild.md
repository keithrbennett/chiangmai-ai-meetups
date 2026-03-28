---
date: 2026-03-27
series: Agents in the Wild
venue: The Kannas, Chiang Mai
duration: 2h 9m
speakers: 6
---

# Agents in the Wild -- March 27, 2026

A Friday session with two substantial presentations: Dave's agentic workflow demonstration and the Agent Language Specification (ALS) framework, bookended by a shorter discussion on agent verification. Geo coordinates on the verification segment confirm The Kannas.

---

## 1. Agent Verification and Sensor Fragility

The session opened with a discussion about the difficulty of verifying agent outputs:

- **The markdown problem:** Personal agent systems work well with markdown files, but agents write "whatever the hell they want" in inconsistent formats. One participant described getting 150 different transcription styles from the same "transcribe this YouTube video" task.
- **Verification is not solvable with more agents:** Having another agent check the output just adds another unreliable layer. True verification requires deterministic code execution -- structured output, schema validation, or compilation checks.
- **Hardware aside:** The conversation briefly detoured into bike sensor fragility. Boundary bikes with large sensors break easily; smaller sensors are more durable. The advice: do not blow into a sensor to test it, and keep water away from it.

---

## 2. Dave's Agentic Workflow and Control Plane

Dave walked the group through his personal agentic operating system, demonstrating multi-terminal, multi-agent coding workflows:

**Named agent roles:**
- **Bob:** Cracks the story (task definition). A digital twin of Bob then validates the story without knowledge of how it was created -- pure context engineering.
- **Amelia:** Handles all development work.
- **A QA agent:** Runs a six-vector code analysis (architecture, code quality, unit testing, and three others), all in background agents.
- **Nateena:** Handles story testing and runs Playwright end-to-end tests.
- **Lisa:** Collects knowledge throughout the process.

**Telemetry and session intelligence:**
- Predicates analyse every conversation for patterns: frustration, repeated prompts, skill formation.
- A unified ingestion system captures telemetry across all agents, though it had not yet been tested on external systems like OpenClaw.
- The system started as telemetry but is evolving into a control-plane application capable of automatic synchronisation.

**Multi-machine synchronisation:**
- Dave works across five computers (two in the Philippines, three in Chiang Mai). Key drop-boxes (shared folders) distribute information across the network.
- Git and shared file systems handle code and brain synchronisation while avoiding conflicts.

**Control-plane UI:**
- A dashboard monitors tools, sessions, and projects.
- Work is segmented into "brains" with librarians that maintain tagged knowledge, perform health checks, and ensure ontology alignment.
- Video recording, chaptering, and AI-driven post-production use transcripts and workflows integrated with external tools.

---

## 3. Agent Language Specification (ALS)

The second half of the session featured a presentation on ALS, a framework for bringing structure to agentic systems:

**The problem ALS solves:**
- Classical software architecture has apps and databases. In agentic systems, skills act as app logic and markdown files act as storage. But without constraints, agents produce wildly inconsistent files.
- ALS adds strict schemas ("shapes") for each module (CRM, invoices, etc.), validation hooks that reject malformed files, and a versioned module structure supporting migrations.

**How it works:**
1. Define entities, modules, and data types in the ALS specification.
2. Validation hooks run on every file write, preventing agents from corrupting data.
3. Natural-language change requests generate migrations and updated skill files automatically.
4. Changes are dry-run on a cloned test copy. Only after compilation and validation pass are they deployed.

**File-system-first philosophy:**
- The presenter argued that agentic search on file systems consistently outperforms database RAG. "People kept coming back to identity file search. It was superior every time."
- Git-compatible file systems enable referential integrity via URI-based entity references.
- MCP servers are limiting because "you're stuck on whatever that function signature is."

**Local search models:**
- The group reviewed a new 20B-parameter local model (from Proma) optimised purely for search and context retrieval, intended to run alongside a larger reasoning model.
- Discussed running it locally with 3-bit quantisation, KV-cache compression for larger effective context windows on limited hardware.
- Use cases: tagging, classification, entity/relationship extraction, semantic matching, re-ranking, and cleaning messy business data.

**Naming debate:**
- "ALS" has unfortunate associations with ALS the disease. The group joked about it and suggested renaming, though no alternative was settled on.

**Broader implications:**
- The presenter framed ALS as "the new high-level language" -- architecture and lifecycle description for software development, where the actual code is "like assembly, we don't care about it anymore, the agents handle that."
- LLMs make large-scale data cleanup and migration dramatically more feasible and cheaper in tokens than traditional developer-heavy approaches.

---

*Session recorded during the Agents in the Wild Friday meetup in Chiang Mai, March 27, 2026.*
