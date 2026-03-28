---
date: 2026-02-21
series: AI Engineers
venue: The Kannas, Chiang Mai
duration: 1h 34m
speakers: 13
---

# AI Engineers -- February 21, 2026

Session at The Kannas with projector available. Around 13 speakers. The organiser led a structured walkthrough of Anthropic's latest releases -- Agents SDK, Claude Code Desktop's new preview feature, plugins, and CoWork as a personal agent platform. A significant portion of the session was interactive, with the group clicking through features together on the projector.

---

## 1. Anthropic Terms of Service & Subscription Clarification

The session opened with a discussion about Anthropic's terms of service, prompted by recent drama around third-party harnesses using Claude subscriptions:

- **Personal use is fine.** Anthropic is "perfectly fine" with individuals using the subscription through the SDK, local harnesses, or experimental setups. They actually want people to experiment.
- **Business reselling is not.** The line is crossed when you turn subscription access into a public offering or let other customers use your subsidised inference. Anthropic is losing money -- users consume $2,000-4,000 of inference on a $200 plan.
- **Open Claude/Open Code fallout:** These projects are problematic because they enable others to benefit from someone's subsidised subscription.

**Sonnet 4.6 as the solution:** Anthropic released Sonnet 4.6 specifically to address the cost problem. It offers most of Opus 4.5's benefits at one-fifth the cost, making it viable for agent systems that would otherwise burn through subscription limits. The group saw this as Anthropic's way of saying "please use cheaper models for agents."

---

## 2. Agents SDK & Claude Code CLI -- Basics for Newcomers

Show of hands revealed ~20% of the room was unfamiliar with the Agents SDK and a few didn't know Claude Code CLI. The organiser provided a quick primer:

- **Claude Code CLI:** Anthropic's internal development tool, the thing that "replaced Cursor." Most of Anthropic's revenue comes from it. Built by Boris.
- **Agents SDK:** A library extracted from Claude Code CLI that lets developers build automated systems with the same mechanisms. If you want Claude Code's power but automated (no human in the loop), you use the Agents SDK.
- **Open Claude** runs on an equivalent of the Agents SDK but open-source.

---

## 3. Claude Code Desktop -- Live Preview Feature (Launched That Morning)

The centrepiece demo. Claude Code Desktop received a new feature just hours before the meetup: the ability to run and preview web apps directly inside the desktop application.

**How it works:**

- Open Claude Code Desktop, select a folder, prompt it to build or run an app.
- The app renders in a preview pane within the desktop app -- no need to manually start a dev server or open a browser.
- Claude creates a config file with "preview" entries (e.g., `dev` for development mode, `preview` for production mode).
- The preview pane takes screenshots of the running app, enabling Claude to visually inspect the output and iterate.

**Live demo:** The organiser built an Airbnb-style app for Chiang Mai experiences that morning with three sentences of input. The group watched it running inside Desktop, noting:

- It supports anything that runs a dev server and loads in a browser (React, Astro, Next.js, etc.).
- Mobile app previews via Expo also reportedly work.
- The tool list includes 13 preview-specific tools (all prefixed `preview_`), separate from the Chrome MCP tools and with fewer, more focused capabilities.
- **Bug encountered during demo:** The preview wouldn't load initially, possibly due to a race condition. Restarting fixed it.

**Claude Code Desktop vs. CLI:**

- Desktop is a visual wrapper around the CLI with a friendlier interface, but missing some power-user features.
- Both have file system access -- Desktop asks for permission but can read outside the selected folder.
- SSH connection feature allows working on remote hosts.
- One participant noted the desktop app is also available on Android and iPhone.

---

## 4. Plugins, Skills, and the Name Collision Problem

Extended discussion on managing plugins and skills at scale, triggered by a participant with a monorepo containing many apps and ~200 skills:

**The collision problem:** Multiple plugins can have skills with the same name (e.g., "front-end design"). Claude only sees the name and description -- if these are ambiguous or duplicated, it gets confused, just like a human developer opening a folder with four identically named files.

**Solutions discussed:**

- **Disable by default:** Use `/plugin` in the CLI to toggle plugins on/off per session. Only enable what's needed for the current task.
- **Edit descriptions:** Most community skills have poorly written descriptions. Edit them to include explicit "use when [condition]" triggers.
- **Gateway pattern (reiterated from previous weeks):** Consolidate multiple same-purpose skills into a single gateway skill with routing logic. The gateway's skill.md is ~20 lines of pointers; the actual content lives in subdirectories loaded conditionally.
- **Project-scoped skills:** Place `.claude/` folders in subdirectories of a monorepo, tying skills to specific apps rather than loading everything globally.
- **Audit before installing:** Most community skills are low-value. One participant: "80-90% of the time, Claude itself is gonna do really focused things without skills." Skills are for patterns you repeat 3-4 times and want done consistently.

**Security warning:** In Open Claude's skills directory, 4-5 of the top 10 community skills contained attack vectors stealing crypto wallets. Recommendation: never install unaudited skills. Use Claude's built-in skill creator to regenerate any community skill from a description.

---

## 5. CoWork as Anthropic's Personal Agent Platform

The organiser demonstrated CoWork (Anthropic's non-developer-facing workspace) and argued it's evolving into their official personal agent platform.

**CoWork plugins are different from Code plugins:** They target non-technical users -- customer support, bio-research for scientists, enterprise search, finance/accounting, and a "Productivity" plugin that manages tasks, plans your day, and builds up persistent memory.

**Live demo of the Productivity plugin:**

1. Installed the plugin, typed `/start`, then `init`.
2. Claude created a file-based personal agent system: working memory, deep memory directory with glossary, dossiers (people), projects, context files, a dashboard, and a task list.
3. Claude then asked questions: "Where do you keep your to-dos? What are you working on? Who's on your team?" -- bootstrapping the memory system from the user's answers.
4. It created company profiles, team member dossiers, and project files based on the responses.
5. The same folder was then opened in Claude Code, demonstrating that CoWork and Code share the same file system and can work on the same project from different interfaces.

**Leaked direction:** At a recent Claude Code event, Anthropic staff reportedly "alluded" to the fact that for the last six months, they've been working on making CoWork a personal agent platform. The organiser connected this to Boris's tweet that "the traditional role of engineering is gone" -- Anthropic's marketing team are engineers, and their engineers do marketing. CoWork is the bridge.

**CoWork vs. Open Claude:** CoWork's advantage is Anthropic's battle-tested permission system, developed for enterprise use. Open Claude has no meaningful permission system and requires community extensions for basic security.

**Remote memory system:** The group briefly noted that Claude Desktop has a remote memory system through Anthropic's API (separate from local file-based memory). "We never talked about it before, but it has a lot of implications -- you can't even peer into that thing."

---

## 6. Zapier MCP & OAuth Security

Briefly discussed: Zapier released an MCP server that handles OAuth connections for services like Gmail, Discord, etc. You can configure it so the agent creates drafts rather than sending directly, adding a human review step.

The group was sceptical: "The worst thing you could hear is 'you're secure, go ahead and feel comfortable.'" New products should be assumed insecure until proven otherwise. The default stance: "No. This is not secure."

---

## 7. Closing & Upcoming Events

- **March 6-7 at 5PM:** A larger event, post-Loi Krathong.
- **Every Saturday:** AI engineering sessions continue (more technical).
- **Every Friday:** Agent-focused sessions also at The Kannas.
- The group went to lunch next door after the session.

---

*Session recorded during "Living on the Frontier" Saturday meetup in Chiang Mai, February 21, 2026.*
