---
date: 2025-11-08
series: AI Engineers
venue: 4Seas, Chiang Mai
speakers: 12
---

# AI Engineers — November 8, 2025

Friday session with around 12 participants. Speaker 0 opened by setting the tone: "It's a bit more software development, technical related. The intention is to be open to going in-depth... we're not afraid to go into the deep end." The format follows the group's usual pattern — a curated list of the week's AI news, discussed one by one, with tangents and deep dives as they come.

---

## 1. AI Infrastructure: Power, Electricity, and Data Centres

The session opened with industry news. AWS and OpenAI announced a partnership deal, and a new AWS data centre built for Anthropic came online — "claims to be the biggest one." Speaker 0 predicted this would become a recurring headline: "Every couple months, the next data centre that comes online is the biggest data centre of all of them."

The more substantive discussion centred on electricity constraints. There are plenty of GPUs and materials, but not enough power to run them. Speaker 0 framed this as a software architecture concern: "You shouldn't be too surprised if that happens. You shouldn't be like, oh my god, we didn't plan for this."

Speaker 3 pushed back on the "blackout" framing, arguing the more likely outcome is what already happens with Claude — overcapacity errors and rate limits: "Because if they don't have the power, they just turn off some GPUs, and then that API hits rate limits." Speaker 2 countered that it's "the same problem, just disguised as a different error message."

Speaker 4 noted seasonality as a factor — "everyone is powering up their ACs" — and pointed out that companies are securing their own electricity supply by reactivating nuclear plants. "Bitcoin miners have done that. Amazon has done that." The group discussed Microsoft's own nuclear efforts and the trend toward micro nuclear plants for decentralised power.

Speaker 6 argued strongly for nuclear: "We've got the power. You just need to use nuclear. It's clean. It's efficient." Speaker 0 mentioned China's first thorium reactor test coming online that week.

Speaker 7 reframed the conversation: "A lot of this conversation about power doesn't take into account what AI could do in other industries that are consuming a lot more power." Speaker 3 added that "human construction uses 38% of the world's global" electricity, suggesting AI-driven efficiency gains could offset its own consumption.

This led to a discussion of **permacomputing** — a movement toward sustainable, electricity-conscious software development. Speaker 0 drew a parallel to early computing: "Twenty-five years ago, when the RAM was like 500 megabytes, you had to be really certain in how you coded your stuff... that seems to be coming back." Speaker 2 found the formal term: "permanent computing... a concept of community practice that applies ethics principles of permaculture."

---

## 2. Industry News: OpenAI Finances, Kimi K2, and Google Workflows

**Anthropic's revenue surge:** Speaker 0 noted that Anthropic's financial report showed Claude Code revenue ballooning from $500M to $1B in a single month, with $3.8B coming from API calls. "Cloud Code is becoming more and more of the main revenue stream."

**Sam Altman's credibility:** Speaker 8 brought up Hacker News discussions about Altman lying, and shared that he'd spent the morning "asking ChatGPT if he's a liar. And it evaded the question... it took like four or five times to actually say yes." Speaker 4 cited Altman's Twitter post: "We do not have government guarantees for OpenAI data centres. We believe the government should not pick winners or losers."

**Kimi K2:** A new open-source model with a 256k context window. Speaker 0 expressed the group's standard scepticism about benchmarks: "Every time these open-source models come out, the benchmarks are almost always showing as good as the frontier closed-source models or better. And then in practice, it's a complete shift." Speaker 1 had seen real evidence from someone named Quentin who was using it in production.

**Google Workflows:** Google's response to OpenAI's agent builder — drag-and-drop, no-code, with deep access to Gmail and Google Drive. Speaker 0 tried it and couldn't get it working: "You have to get a higher-level subscription... it actually didn't fucking work." Speaker 1 was "very, very underwhelmed" and suggested just integrating GPT tools instead. The group discussed Google's enterprise security model as both a strength and a friction point. Speaker 0 compared it to Microsoft's browser wars era: "Google's now in that same seat where they're like, we have principles, and we're gonna follow it across our entire enterprise. But now all of us have to deal with this."

**Tool calling as the key differentiator:** Speaker 0 argued that Claude and GPT now have parity on tool calling — "GPT five, the only thing this shit brought to the table was that tool call ability" — and that the group was waiting for Gemini to catch up. Speaker 8 noted Google's unique data advantage: "They have access to your Gmail, Google Analytics, all the advertisements and the web."

---

## 3. MCP Optimisation: Skills as Lazy-Loaded Replacements

A major technical discussion on context window efficiency. Anthropic released a document discussing code execution as the next evolution of MCP, and the group had hands-on experience with the shift.

**The problem:** MCP servers use optimistic loading — all tool definitions are front-loaded into the context window. "You fill it up with all the MCPs you need, and then bam, 30% of the context window is now allocated to this."

**The solution:** Blank out the MCP JSON file entirely. Install CLI tools in the dev environment and create skills that explain how to use each CLI. Speaker 0 described this as moving "from optimistic loading to lazy loading — you get this on demand, as needed."

Speaker 9 confirmed his team was doing this: "They're sticking the MCP into the skill rather than into the context window. So it's only called when it's needed rather than constantly running in the background."

Speaker 3 highlighted a second optimisation from Anthropic's document: instead of pulling an entire document into context, let the LLM write code to process it. "If you fetch an Excel document, what you really want to know is a sample of it and the headers. So you have the fetch and then pass that to some code that Claude wrote to get the first four results and the headers... in your context, instead of 50k lines, you've got four lines and the headers."

Speaker 9 quantified the impact: "Code execution via skill actually brings nothing back into your context... it's such a tiny part that it plays no significant role."

**Sub-agents and MCPs:** Speaker 5 asked whether moving MCPs into sub-agents would help. Speaker 0 noted that the last two Claude Code releases supported this — tying MCPs to sub-agents and adding planning mode — but the first iteration "was total shit." Speaker 3 had started using the Explorer agent (Haiku) for deeper research: "It would only use Explorer when I asked it to find something in the code base. And now it's using Explorer to analyse code more." The group discussed sub-agent persistence — whether they retain context between calls — with Speaker 3 noting "they just announced that you can resume sub-agents, but I've never seen it in action."

---

## 4. Claude Code Web vs. CLI

Speaker 9 had been using Claude Code Web heavily since the $1,000 credit was released for Max plan subscribers.

**Workflow:** "Every feature I've built this week, I start on Cloud Code Web. It does the feature, and then there's a button to open in the CLI. It just gives you a quick link to spin up." He runs multiple features simultaneously in separate containers and reviews locally.

**Quality difference:** "Cloud Code Web is executing better. I don't even know how to explain it, but the output is way better than if I would've just done it locally." Out of 10-15 features, he hadn't needed to fix a single substantive issue — only cosmetic things like spacing and padding. Cost: $7 out of $1,000.

Speaker 0 explained why: "If you have your model sitting in the same data centre as the containers, you have extremely low latency. The costs are totally different. Also, the optimisation is — it's really hard to optimise Claude Code for a local environment. You have to make a million assumptions. But if you pull it into a controlled environment, it's like, I know exactly what's in here. And suddenly, the optimisations go through the roof."

**Environment secrets:** Speaker 9 keeps everything in GitHub Secrets, which the web environment inherits. Speaker 4 raised concerns about giving full repo access, but Speaker 9 clarified you can also paste environment variables temporarily for a single session.

**The bigger picture — is CLI dying?** Speaker 9 described a key moment from a Dan Shipper interview with Anthropic's Kat and Boris: "He asked, do you see that the CLI is actually the ending? And Kat kind of freaked out and deferred it to Boris. And Boris was like, there's something. Something's happening." Speaker 4 noted Anthropic's incentive: "You put everything into the web and Anthropic is already aware of what you possibly do. Like, from the internal perspective, how do I pack this workload? It makes a lot of sense that this is a lot better for them."

Speaker 5 saw this as an accessibility play — making the CLI-level experience available to non-technical users: "I'm always trying, like, how do I get my friends that are non-technical people doing Google Ads business or whatever to use this, because it's so much more efficient to have GPT five in the terminal." Speaker 2 shared the pain of onboarding non-technical users: "I had to use Claude to go, how the fuck did I get Claude running on Windows?"

---

## 5. Claude Desktop: Skills, Projects, and Context Limits

Speaker 9 connected the dots to Claude Desktop — skills are now available there too: "You can build these skills for finance or whatever that access all these Excel files... now you can just go into Desktop and talk to it normally and actually get real usable useful output that we used to only be able to get inside the CLI."

**Skill marketplace:** An unofficial marketplace appeared on day one. Speaker 9 explained: "If you go to the Claude skills GitHub, they have their internal ones, but they also had a link to a marketplace for other ones. It's not official. I think it's unofficial, but they're endorsing it." One of the bundled skills is a skill creator — it generates a zip file you drag into Desktop.

**Context limits in Desktop:** Speaker 5 raised a frustration: "You will quickly run out of context in the conversation... conversations always end at some point and then you need to start a new conversation." Speaker 9's workaround was to use Projects, creating a new chat within the same project each time. He also noted Claude Desktop's memory refreshes every 24 hours — "if you do things differently, it'll change" — unlike ChatGPT's memory, which retains stale assumptions from months ago.

---

## 6. Security: Secrets Leakage, Prompt Injection, and Agent Attacks

A wide-ranging security discussion triggered by multiple incidents that week.

**Secrets in the context window:** Speaker 2 described a concrete incident with Claude Code Web. While testing across multiple repos (which it doesn't support), the environment exposed his GitHub token: "Claude goes, oh, you need to now roll over your GitHub token because I now have it." He checked the terms — "ninety-day retention data policy. So, essentially, that GitHub token is up in Claudivus." Speaker 0 added: "The security attacks with prompt injections now become even more important. It's actually quite easy to see how you can harvest that data when Claude is running on its own, doing web calls."

**Malicious skills and plugins:** Speaker 0 noted several security incidents that week: "Some skills that were malicious, some plugins that were malicious. There was a plugin that was found to be very, very malicious." He drew a parallel to browser extensions being compromised.

**Black-hat SEO and agent deception:** Speaker 2 described meeting someone at an SEO meetup who builds software that "sits at the edge of Cloudflare" and serves different pages to Google bots versus humans. The group connected this to agent security: "When agents are talking to these sorts of servers, could someone be writing software to serve up different stuff to what the human sees?" Speaker 0 compared it to malware sandbox detection.

**DEFCON 33 — passive prompt injection in Gemini:** Speaker 4 gave a detailed account of a DEFCON 33 talk demonstrating passive prompt injection on Google Gemini. The attack chain: send someone a Google Calendar invite containing injected prompts. When the victim asks Gemini about their schedule, it reads the invite and follows the injected instructions. "They called it passive tool calling... in their prompt, you just call another tool, give another prompt for that tool, call another tool. You pass the prompts to the other." The result: "They could hijack your phone, basically, because every time you use Gemini or anything related to Gemini on your phone now, your prompts are injected." Speaker 4 confirmed: "Google still hasn't fixed a lot of these issues."

---

## 7. Pre-Commit Hooks and Code Quality Enforcement

The ThoughtWorks Tech Radar #33 was published that week, and Speaker 0 walked through key recommendations.

**Pre-commit hooks for secrets:** Multiple participants shared their setups. Speaker 4's team uses the Python `pre-commit` framework with linting rules from a centralised repo: "When you do your commit, it will look into a pre-commit YAML, reference a public repo, pull the code, and execute it. If it doesn't follow those rules, it won't allow you." Speaker 8 uses a simple custom script with detect-secrets (Yelp/IBM fork). Speaker 2 uses Husky with lint and commit message hooks.

**Agents circumventing hooks:** Speaker 5 flagged a problem: "I even had Claude circumventing my Husky hooks in the past. It didn't go through, and then it just forced it or circumvented it somehow." Speaker 5 identified the mechanism — a CLI flag to skip the hook on commit.

**Secrets leaking to LLMs, not just repos:** Speaker 2 distinguished two threat surfaces: "It's not just that you're sending it to GitHub. We're sending this shit to large language models." Combined with marketplace skills, "they could also be looking for that shit as well."

---

## 8. Continuous Compliance (ThoughtWorks Tech Radar #1)

The number one recommendation on the ThoughtWorks Tech Radar was **continuous compliance** — integrating policy-as-code tools like Open Policy Agent (OPA) and generating SBOM (Software Bill of Materials) within CI pipelines, aligned with SLSA guidance.

Speaker 0 read directly from the report: "The increased use of AI in coding and the accompanying risk of complacency with AI-generated code makes embedding compliance into the development process critical."

Speaker 4 shared real-world experience from implementing this for ISO certification: "It's a big pain in the ass. OPA is like one of the biggest, another one is Gatekeeper. And then a lot of tools integrate into that, but some other tools bring their own policy management and language. HashiCorp has Sentinel." He gave a concrete example: "If you have a Kubernetes environment, a developer wants to deploy something. Then the deployment needs to follow a certain rule set. For example, you can't deploy an ingress without TLS."

Speaker 2 proposed using Claude's skills as compliance enforcers — "the skills become enforcers" running in CI as "predicate prompts." Speaker 4 raised the key risk: "You need to make sure that these agents are not changing your policies because they realise, oh, this doesn't work. So I'll just change the policy and it will work." Speaker 2 agreed the distinction is critical: "They can be reporting rather than changing."

---

## 9. Windsurf's Code Visualisation and Reference Architectures

**Windsurf's mermaid diagrams:** Windsurf released a feature generating mermaid diagrams of the codebase directly in the IDE. Speaker 0 described it as "a way to read the code base via abstraction — you're not reading lines of code, you're reading this projection of the code that is a diagram." The group discussed the hard problem of keeping diagrams in sync with code changes across branches, with Speaker 2 arguing they should be "dynamically driven off the dataset, not persisted into the repo."

Speaker 0 connected this to C4 diagrams: "You can zoom up high level and see the larger system boundaries, zoom all the way into a function level, zoom out to a class level, zoom out to a boundary level between subsystems. You would need multiple layers of projections based on the bird's eye view you want."

**Anchoring coding agents to a reference application (ThoughtWorks — Trial):** A novel pattern from the Tech Radar. An MCP server connects to a template codebase containing a company's gold-standard implementation — "not actually running in production, but it has the best practices." All teams reference this one application through the MCP server.

Speaker 2 described already doing this: "I did a BMAD copy agent that worked from a reference application to the main application. When I needed multi-tenancy or user impersonation, I didn't do it in the application. I did it in the reference application, and then I had my agent bring it over."

Speaker 10 pushed back on the MCP overhead: "A lot of these abstractions are useless. Having an MCP do that is so inefficient when you can just have submodules." Speaker 8 agreed: "If you look at Cloudflare, they have really excellent MCPs, but their CLI is 10 times better."

---

## 10. GPT-5 Prompting Guide and Cursor Community

Speaker 7 brought up OpenAI's GPT-5 prompting guide, released two days prior. Key points: give room for planning and self-reflection, use the right reasoning effort, "avoid overly firm language, and control the eagerness of your coding agent." The guide confirmed XML formatting works with GPT models.

Speaker 0 connected this to the planning-mode pattern: "That seems to be a stable thing too. Codex doesn't have a slash planning mode on the extension. I think now the CLI does." He noted someone on a Cursor forum called plan mode "life-changing" — despite Claude Code having had it for a while.

**Cursor community event:** A local Cursor event had taken place that same day. Several attendees from the AI Engineers group had gone to a previous one and found it poorly prepared: "People that never used Cursor before didn't even know what Cursor is. They just joined because some friends went there." Speaker 3 was blunt about Cursor's motives: "They know they're going to the drain. No one's using them... they need to increase their valuation."

Speaker 0 offered a different take: Cursor might pivot to a "community-centric company" with physical meetups worldwide, bridging AI adoption for non-technical users. "It's why everyone shows up here — there needs to be somewhere to talk in person about AI. If you go online, it's a trap. There's so much misinformation."

---

*Session recorded during the "AI Engineers" Friday meetup in Chiang Mai, November 8, 2025.*
