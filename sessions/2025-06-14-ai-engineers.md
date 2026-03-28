---
date: 2025-06-14
series: AI Engineers
venue: Morestto, Chiang Mai
---

# AI Engineers — June 14, 2025

The atmosphere was more subdued this week, with conversations happening in smaller, focused groups. The discussion was a mix of practical tools and more philosophical questions about the future of software development.

## Key Technical Concepts & Strategies

- **LSP (Language Server Protocol):** A term that came up, which refers to the protocol used by IDEs to provide features like code completion, definitions, and suggestions.
- **A New IDE Paradigm:** Nick, the facilitator, discussed his project to build a new type of coding environment. The idea is that as agents handle most of the coding and Git operations, the developer's role shifts. The new "IDE" becomes less about writing code and more of a supervision platform for overseeing and managing multiple agents.
- **git worktree for Parallel Agents:** A practical solution was shared for running multiple agents on the same codebase simultaneously. By assigning each agent its own git worktree, they can operate in isolated branches without interfering with each other. The results can then be merged later.

## Tools & Platforms Mentioned

**Google Tools:**
- JULES (jules.google): A Google product worth investigating.
- Stitch (stitch.withgoogle.com): A new beta tool, likely for building front-ends with AI.

**Data & Backend:**
- PG Vector: A powerful PostgreSQL extension that adds vector database capabilities, making it easy to build AI applications on top of a standard Postgres database.
- Supabase: It was confirmed by the group that self-hosting Supabase is viable and should provide all the same features as the cloud version, making it a good option for projects requiring specific data sovereignty (e.g., hosting in a German data center for German clients).

**Crawling & Automation:**
- Crawl4AI: An open-source, LLM-friendly web crawler and scraper.
- Playwright MCP & Puppeteer: Mentioned again as essential tools for agent browser automation.
- Figma MCP Plugin: A plugin that allows an agent (like Cursor AI) to interact with Figma designs, view UI elements, and assist in debugging.

**Prototyping & Utilities:**
- Firebase Studio: A tool for rapid prototyping, similar in purpose to Vercel's V0.
- Claude Squad: Mentioned as an option for orchestrating multiple agents.
- Yazi: A very fast, Rust-based terminal file manager.

## Post-Meetup Lunch & Bruno's Open-Source Business Stack

The conversation at lunch with Bruno, a YouTuber and SEO specialist from Brazil, shifted towards the practicalities of running an online business with a fully open-source stack.

**Bruno's Business Model:** He acquires expired domains that have existing backlink authority, rebuilds the sites using the Wayback Machine to maintain their original appearance, and then sells backlinks from his network of ~300 websites.

**Bruno's Self-Hosted Open-Source Stack:**
- Project Management: Huli.io (a Notion/Jira/Linear alternative)
- Email Marketing: Mautic.org
- Chatbots: Typebot.io
- WhatsApp Integration: Evolution API
- Customer Support Hub: Chatwoot.com (integrates Telegram, WhatsApp, Messenger, etc.)
- Email Sending: SendGrid API is used to send emails from Mautic

## Personal Reflections & Future Strategy

The day's conversations sparked a deep dive into personal strategy, focusing on a potential pivot from a traditional agency model to a more scalable business.

**The Agency vs. Education/Community Business Model:**
- The AI Agency: Potentially high-ticket ($10k+/automation), but difficult to scale, hard to generate qualified leads, and involves complex client management. Maintaining bespoke N8N workflows for multiple clients is a significant challenge.
- The Education/Community Model: More scalable and simpler to manage with a subscription model (e.g., 50 members at €50/month = €2,500 MRR). This model aligns better with the enjoyment of teaching.

**Proposed YouTube Strategy (1-Month Test):**
- Channel 1 (For Business Owners): Create superficial content focused on benefits ("save time, make more money"). The goal is to attract high-value agency leads by speaking their language, with a clear call-to-action to book a consultation.
- Channel 2 (For Builders): Create in-depth technical tutorials. The goal is to build a community of people who want to learn and build for themselves, creating a funnel for the paid community subscription.

**The Personal Knowledge Base Project:** A core passion project is to create a personal database by documenting as much of life as possible (e.g., transcribing voice memos). The goals are to feed this data to an LLM to act as a personal coach, analyze recurring problems, create an authentic content generation pipeline, and train an AI to resemble your personal communication style.

## Resources & Actionable Next Steps

**Book Recommendations (from Bruno):**
- DotCom Secrets (2015) by Russell Brunson
- Traffic Secrets (2020) by Russell Brunson
- Key Insight: These books can be loaded into an LLM to extract frameworks and use them in system prompts to improve AI workflows.

**Immediate Action Item:** An attendee at the meetup was interested in an N8N workflow for invoice processing. The plan is to build a version of this workflow this week, find the person at the next meetup, and offer to set it up in exchange for a first testimonial for marketing purposes.
