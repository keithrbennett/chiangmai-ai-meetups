---
date: 2025-08-09
series: AI Engineers
venue: 4Seas, Chiang Mai
---

# AI Engineers — August 9, 2025

This week's discussion was a deep dive into the practical and philosophical differences between GPT-5 and Claude, evolving developer workflows, and the changing role of the software engineer.

## GPT-5 vs. Claude: Instruction-Following vs. Ambition

- **GPT-5: The Precise Instruction-Follower.** Extremely literal, does exactly what told. Superior for large, complex codebases where unexpected changes are dangerous.
- **Claude: The Ambitious Problem-Solver.** Goes beyond the explicit prompt to solve perceived underlying problems. Sometimes adds unrequested features but occasionally discovers valuable, unplanned features.
- **The Context Window Trade-off:** GPT-5's literalness leads to less context consumption. Claude's ambitious nature fills the context window faster.
- **Unanimous consensus:** For development tasks, instruction-following is far more valuable than raw intelligence.

## "Model Intimacy" and The GPT-5 Learning Curve

Developers have subconsciously learned how to prompt Claude. Using the same style with GPT-5 fails because it requires a different, more explicit communication style. Prediction: after 200+ hours of use, the narrative around GPT-5 will flip from disappointment to success.

## New Tools and Platform Updates

- **Claude Code GitHub Actions:** Autonomously scans for errors, improvements, and security vulnerabilities, automatically creating detailed PRs.
- **Gemini CLI for GitHub Actions:** Free, used for rapid prototyping and testing agent logic cycles before plugging in more expensive models.
- **Multi-Model Workflows:** Tools like OpenCode now allow assigning different models to different sub-agents within the same project.

## The "Black Box" Problem & Debugging Strategies

When an issue occurs in production, the original LLM session is gone. Solutions discussed:
- Verbose Logging
- Sequence Diagrams for complex call stacks
- Centralized Logging Stacks (ELK Stack, OpenTelemetry)
- Error Analytics via Google Analytics

## The Evolving Role of the Developer

Developers are transitioning from hands-on coders to managers of agents, architects, and dev managers. Value is no longer in writing every line of code but in breaking down complex problems, defining robust architecture, and setting clear guardrails for AI teams.
