---
date: 2025-10-18
series: AI Engineers
venue: 4Seas, Chiang Mai
---

# AI Engineers — October 18, 2025

The meeting focused on the practical implications of model selection, Claude's new skills system, and strategies for managing the relentless pace of tooling changes.

## Model Comparisons and Use Cases

- While Haiku is cheaper per token, it uses substantially more tokens — real-world cost savings aren't straightforward.
- Newer models trained to purposefully use their full context window to be less "lazy."
- The small model "scraping" problem: extracting data from thousands of pages at scale with context-limited models.

## Claude Skills Explained

- Best understood as deterministically-run sub-agents defined in a Markdown file
- Give the entire Claude ecosystem the ability to run bash commands and file system operations in a sandboxed container
- Packaged as zip files with compressed descriptions; agents load full context only when needed
- Target audience: non-developers, enabling "Claude Code-like" capabilities for all users

## Developer Productivity and "Tooling Anxiety"

- **The DORA Report:** "Speed vs. stability trade-off is a myth" — but the group suspected the missing variable is cost (small groups of expensive 10x developers).
- **Coping Strategies:** Project-based focus (heavy exploration at project start, declining to zero), the "underwater" strategy (ignore all new tools until project ships), and community sourcing.
