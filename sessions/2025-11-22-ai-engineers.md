---
date: 2025-11-22
series: AI Engineers
venue: 4Seas, Chiang Mai
duration: 1h 42m
transcript: ../transcripts/2025-11-25-unknown.md
---

# AI Engineers -- November 22, 2025

Saturday session with around 10 participants. A quieter news week, but the session was dominated by announcements about an upcoming Anthropic-sponsored Claude Code event and extended discussion on practical workflows, rate limits, model comparisons, and the hierarchy of Claude Code automation primitives (slash commands, skills, agents).

---

## 1. Anthropic-Sponsored Claude Code Event -- December 20 at CMU

Speaker 0 opened with the big announcement: Anthropic released a form inviting community hosts worldwide, and one of the group's members -- Ian -- was selected as the official Anthropic-sponsored host for Chiang Mai and Bangkok.

**Event details:**
- **Date:** December 20, 2025
- **Venue:** Chiang Mai University (CMU), chosen for capacity -- expected to exceed 100 attendees
- **Content:** A message from Dario Amodei, videos from Boris and Kat (the designers of Claude Code), plus unreleased material: "stuff that basically the public isn't aware of, or I don't even know if they're gonna be aware of"
- **Format:** Still pending final guidelines from Anthropic. The organisers want to include community presentations but need format approval first. A submission form was shared for anyone wanting to present.
- **Presentation requirements:** Must be about Claude Code specifically -- no other companies. Talks should cater to a range from beginners to senior engineers, not exclusively advanced topics.
- **Bangkok event:** A separate event planned at the AWS office, leveraging Speaker 1's existing venture capital partnership with AWS. "They'll sponsor it. I don't wanna pay anything out of my own pocket."
- **Perks:** Speaker 1 disclosed that attendees would receive free Anthropic credits.

Speaker 3 requested that presentations include topics beyond coding -- "daily life automations that maybe you run, workflows, stuff like that."

---

## 2. Anthropic Interviewer Tool

Speaker 0 flagged a new tool called "Anthropic Interviewer" that appeared during the week -- a web-based questionnaire designed to extract domain knowledge from professionals.

**The shadow IT analogy:** Speaker 0 compared it to the classic enterprise scenario where a non-developer builds a complex Excel workbook that effectively runs part of the company ("an Excel sheet with 30 sheets at the bottom, a sequential app"), and then IT sends in developers to interview that person and extract their domain knowledge to build a proper system. "I think this is a replacement for that. It's a replacement for the human who goes in and tries to take that info to build something useful for the company."

**Group reaction was mixed:**
- Speaker 2 asked whether it sends data only to Anthropic or whether users can use it with their own clients -- no clear answer
- Speaker 4 had already completed it: "I got duped into it... it was more like them getting some product feedback perhaps." It asked what he wanted to use AI for and where he was unhappy with it
- Speaker 3 argued it could be useful: "it could also be useful to us if we provide the right feedback and then they make the product better for us"
- The creator was identified as an external consultant, not an Anthropic employee, though Anthropic adopted the tool

---

## 3. Anthropic's Internal Efficiency Data

Anthropic released internal data comparing developer efficiency across model versions. Key findings discussed:

- **Tool call reduction:** Older models (Sonnet 4 / 3.5) would make around 60 tool calls per task; Opus 4.5 completes the same tasks in 40 or fewer calls
- **Across-the-board improvements** in task time and token efficiency
- Speaker 6 noticed a specific change: code exploration sub-agents switched from Haiku to Sonnet 4.5

---

## 4. Sub-Agents and Multi-Agent Workflows in Claude Code

Speaker 0 described experimenting with explicitly keywording sub-agents into prompts -- something he previously avoided because "it was terrible" with earlier models but now works well with Opus 4.5.

**The experiment:** A large enterprise feature that he attempted as a one-shot. He manually decomposed the spec the way he would if managing multiple Claude Code sessions, then instructed the parent LLM to spawn eight Opus sub-agents and distribute the work the same way. "It got it right. Kinda. It wasn't perfect, but it was really close. It took forever -- a thirty, thirty-four minute long thing. And it ran sub-sequentially. It was super cool. I had an AGI moment yesterday."

Speaker 2 described a complementary approach -- using skills to create handover conversations between agents: "The goal is to know how to talk to the two agents so it does a handover conversation. You're not polluting one conversation with another conversation, but you've got this natural communication stream." He leveraged the built-in create-skill command from Anthropic, which "generates a template and forces Claude Code to review the template and then modify the template and send questions back to you."

**Skills built from CLI documentation:** Speaker 2 built skills for a digital asset management (DAM) tool by feeding in CLI help documentation rather than source code. "It's the documentation of the CLI tool because that's how I would use it." Speaker 3 confirmed the pattern: "You build the documentation into the help and then ask it to explore the CLI through the help instructions?"

---

## 5. Opus 4.5 -- Trust and Quality

Multiple participants noted a step change in trust with Opus 4.5.

Speaker 2 had spent an entire week vibe-coding a video content application, recording each session: "I built a whole application all week. Every time I build another session, I recorded it." The app evolved over seven days to handle transcription, project routing, YouTube chapter headings, and graphics generation.

Speaker 3: "Since Opus 4.5 came out, it's doing such a great job that I feel like how much more significant rework I had to do every time... right now, almost was always perfect the result."

Speaker 2 agreed: "Sometimes it goes around holes, but generally it's awesome."

---

## 6. Rate Limits and Pricing Tiers

Extended discussion on the $100 and $200 Max plan rate limits.

**The trigger:** Speaker 2 was getting rate-limited again despite the recent improvements. The cause: switching from two projects in separate terminals to one project with three or four concurrent agents. "I was really curious to hear you talk about sub-agents going, oh my god, that would hit it even harder if you were running eight."

**Opus usage tracking removed:** Speaker 0 discovered that the separate "Opus usage" indicator in the dashboard had been silently removed and unified: "I checked yesterday. It's totally gone. It's unified... I was upset because they didn't announce that."

**Token efficiency observation:** Speaker 1 reported a dramatic token reduction on a specific task -- from 39,000 output tokens previously to just 599 tokens for the same task with 47-48 tool calls and hundreds of megabytes of documents. The group was uncertain whether this was a bug or a genuine optimisation.

**Practical advice on tiers:** Speaker 7 suggested starting at $100 and downgrading to $20 if limits aren't hit. Speaker 3 confirmed mid-cycle upgrades are prorated.

---

## 7. Model Comparisons -- Claude Code vs. Gemini vs. Copilot

**Gemini for Rust/Go:** Speaker 0 hypothesised that Google's internal language preferences (Go, memory-safe languages) influence Gemini's RLHF training, making it stronger for Rust and Go but potentially weaker for TypeScript. He cited a talk by Ilya Sutskever with Garshwa about how RLHF creates "hyper specificity" -- models that excel at specific tasks but suffer elsewhere.

**Claude Code vs. Copilot:** Speaker 5 was frustrated that his company uses Copilot: "You're using Opus 4.5 in Claude Code and in Copilot, and it's absolutely not the same. You can tell how much more powerful Claude Code is. It knows better how to use the underlying model."

**Context7 MCP issues:** A coworker of Speaker 5 crashed Copilot repeatedly by pulling in too much context from Context7, which bundles entire product documentation into single massive files. Speaker 6's workaround: "Limit the context to four or 8,000. Use it like a Google search. Put the query string you're interested in, use this amount of tokens, and see if it's helpful."

Speaker 6 had largely stopped using Context7: "It really depends on who curated the specific file... a lot of times, the answer is no." Speaker 7 noted that llms.txt is emerging as a better pattern -- websites now provide LLM-specific markdown files, and agents can be redirected to those automatically.

**MCP turns one year old:** Speaker 5 noted that MCP had just celebrated its first anniversary (mid-November 2024 launch), which the group found remarkable given its ubiquity.

---

## 8. The Slash Commands -> Skills -> Agents Hierarchy

An extended practical discussion on how to structure Claude Code automation, triggered by Speaker 9 asking about the difference between BMAD agents and skills.

**Speaker 6 laid out the progression:**
1. **Start with slash commands:** "If you notice yourself writing the same prompt all the time, just add it to a slash command"
2. **Graduate to skills:** "If you notice you have to do one slash command and then another in a row, maybe move those into a skill"
3. **Then agents:** "If you're using multiple skills, maybe then you write an agent, and the agent has these two skills"

"Start low, work your way higher. Start with slash commands. Don't get bogged down."

**Speaker 5 reinforced this with a pragmatism warning:** "Just because other people are doing it or tell you this is best practice doesn't mean it's good for you... I can spend a week to improve it and save five minutes a day, but is it really worth it?" Speaker 6 agreed: "Just start fucking doing shit... if you notice you're doing the same things repeated, slash command. Start there."

Speaker 3 suggested an in-conversation approach: at the end of a session, ask Claude whether recurring patterns should be extracted into CLAUDE.md instructions or slash commands.

---

## 9. Claude Web for Non-Technical Teams

Speaker 6 described using Claude's web interface to create guided contexts for non-technical team members -- similar to Gemini Gems but with better sharing: "If you're the developer and you're working in a company with non-tech people, they added the ability to do what I would call Gemini gems -- context, prompts, and then share with your team."

**Use cases:**
- A copywriting context that scores sales copy and provides ranked variations ("Your copy's a four. Here's ones that are eights and nines")
- A Figma guide for a designer who only knew Illustrator, built via deep research
- A design review prompt where designers post URLs and the agent checks against known issues before escalating to the human

Speaker 1 connected this to Claude Desktop skills: "You can share skills inside Claude Desktop... you can share chat." Speaker 6 confirmed skills can be attached to these shared contexts.

Speaker 1 also noted Anthropic's own blog posts about internal non-coding usage: "Their marketing departments and their HR, these aren't coders, but they're still using Claude Code every day."

---

## 10. Evals, Observability, and Tech Debt

**Evals as error flagging:** Speaker 6 reframed evals as fundamentally simple: "Evals to me is just flagging obvious errors and then trying to bring attention to you where problems are. That's all it is." He cited a BrainTrust founder's point that eval metrics are often meaningless -- "oh, my eval's at 70% -- they're just traces, and you've invented some metric." The only objective measures are concrete outputs like pulling the right price.

**Refactoring with AI:** Speaker 8 argued for spending significant time on continuous refactoring when working with AI: "Easily 20%, that's been high, a lot of time on refactoring code that I write. Because with AI you produce so much so quickly that I need to have the feeling I know what's happening." Speaker 0 suggested those repetitive refactoring prompts are natural candidates for slash commands.

**Automated quality gates:** Speaker 3 described adding complex linting rules (file size limits, cyclomatic complexity checks) as pre-completion checks, so Claude notices problems before declaring a task done and reflexively refactors.

**Spec-driven development from Anthropic:** Speaker 6 mentioned a paper or blog post suggesting Anthropic would natively support spec-driven development in Claude Code for longer-running agent development, though he couldn't locate the source.

---

## 11. Quick Hits

- **Google DeepMind dynamic learning during inference:** Speaker 4 saw a post from DeepMind research leads claiming they "cracked dynamic during inference" -- changing the model at runtime rather than relying on static weights. No details on the method. Speaker 0 was sceptical: "I've heard of hundreds of breakthroughs in papers... when do we see that?"
- **Dev containers and remote Claude Code:** Brief discussion of running Claude Code in dev containers on AWS infrastructure, SSH-ing into dev pods. Speaker 0 noted Cursor and VS Code support this but Zed does not.
- **Anthropic smart contract paper:** Mentioned but not discussed in depth -- Anthropic published research on extracting $3.1 million from smart contracts hypothetically.
- **Codex (OpenAI):** Speaker 0 polled the room -- no one raised their hand for using Codex, which he called "code red" for OpenAI.

---

*Session recorded during "Living on the Frontier" Saturday meetup in Chiang Mai, November 22, 2025.*
