---
date: 2025-10-25
series: AI Engineers
venue: 4Seas, Chiang Mai
---

# AI Engineers — October 25, 2025

The meeting was an engineering-centric discussion covering the week's AI news, with a particular focus on agent browsers, AI content authenticity, security, and new developer tools.

## GPT Atlas: The New AI Browser

- An AI-native browser with an "Agent mode" that can autonomously navigate websites and perform tasks
- Works "90% of the time," only failing on older or very complex sites
- Competing with Microsoft's Co-Pilot Edge and Google's "Product Mariner"

## Security and Prompt Injection

- Members expressed distrust for sensitive tasks like banking
- Hidden prompts in images or URLs can trick agents into navigating to other sites and exfiltrating data
- Simon Willison's Rule: "Anybody who can get their tokens into your context should be considered to have full control of what your agent does next"

## AI-Generated Content and Watermarking

- Companies embedding steganographic watermarks into AI-generated images, videos, and text
- Model Poisoning (Nightshade): altering pixels invisible to humans that corrupt AI training

## New Developer Tools

- **OpenSpec:** "Opinionated" workflow — developer writes a "proposal," OpenSpec generates a detailed "change," then implements after approval. Completed in 30 minutes what took Devin 8 hours.

## Claude Skills / Token-Efficient Context

- Skills are deterministically-run sub-agents defined in Markdown files
- Give the entire Claude ecosystem the ability to run bash commands and file system operations in a sandboxed container
- Packaged as zip files with compressed descriptions; agents load full context only when needed
- Target audience: non-developers, enabling "Claude Code-like" capabilities for all users
