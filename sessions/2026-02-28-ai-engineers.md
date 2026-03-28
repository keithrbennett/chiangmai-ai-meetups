---
date: 2026-02-28
series: AI Engineers
venue: Darkstar HQ, Chiang Mai
duration: 31m
speakers: 6
---

# AI Engineers -- February 28, 2026

A compact Saturday session covering organisational memory, agent identity, remote development tooling, and the geopolitics of military AI contracts. Around six speakers across five recorded segments, with discussion flowing freely between topics.

---

## 1. Context Graphs and Organisational Memory

The group explored the idea that current systems of record capture what happened but not why decisions were made. A participant gave the example of a customer-service agent making an exception for a loyal customer -- the CRM logs the outcome, not the cultural norm that drove it. The proposed solution: a **context graph** that preserves reasoning, intent, and distributed cognition behind actions.

Key points raised:

- **Distributed cognition:** Companies form shared intuitions about what is acceptable through countless small decisions. These norms are cultural and rarely documented.
- **Engineering challenge:** Where does the data come from? Journaling, manager-employee interactions, and meeting transcripts were suggested as inputs. Integrating these into a graph structure that feeds into other systems would create genuine organisational memory.
- **Executive visibility:** A CEO could use a context graph to evaluate not just outcomes but decision quality across the organisation.
- **Related concepts:** The group mentioned dollar graphs, graphite, and a newer buzzword -- "Vexcrats" -- as adjacent ideas in this space.

---

## 2. Authorising and Identifying AI Agents

A brief but pointed discussion about how humans should verify which AI agent system they are interacting with. One speaker argued that before trusting an agent online, you would want an in-person signal or transaction -- some kind of handshake -- because "there are millions of agents and I don't know who they belong to."

This tied back to a previous Friday session (Agents in the Wild) where the same question had been raised. The consensus was that the problem is real but nobody has a clear solution yet -- particularly for someone running a single personal agent who does not yet need to federate with others.

---

## 3. Remote Development Environments

The group discussed practical workflows for always-on remote development:

- **Claude Code CLI + slash command:** One participant demonstrated that typing a specific command in the Claude Code CLI generates a URL. Opening that URL on a phone gives access to an online server that never turns off.
- **AWS remote containers:** The same workflow extends to spinning up a remote container on AWS, opening Claude Code inside it, and enabling remote control. This was described as a long-standing personal workflow.
- **Terms-of-service concern:** Another participant flagged that this approach might violate provider ToS, though no definitive answer was reached.

---

## 4. Anthropic's Military AI Contract Refusal

The longest segment of the session. Anthropic declined to sign a Department of Defense contract that OpenAI had accepted (reportedly in November). The group dissected the details:

- **The distinction:** Anthropic is not opposed to its models being used for targeting systems (identifying targets). What they refused is allowing their AI to operate at the point of target -- the final autonomous action. "They don't want their AI to be used at the time of the target."
- **OpenAI's position:** OpenAI signed the same contract. The group noted that the DoD is already using Anthropic's models, making the refusal partly symbolic.
- **PR angle:** Some participants suggested Anthropic's AI safety lab is skilled at generating headlines, and this may partly be a public-relations move. "They've already been working with [the government]."
- **Real-world drone warfare:** A participant who works on open-source Chinese camera firmware explained how YOLO object-detection models already run on repurposed consumer cameras in Ukraine/Russia drone warfare. When electronic warfare jams the data link, onboard AI handles the last mile of targeting autonomously. "You see the YOLO HUD in the videos they release."
- **Supply-chain risk:** The group speculated that if a company refuses military use, the government could apply pressure or even threaten to take control under national security claims.

---

## 5. The Value of Unknown Unknowns

The session closed with a reflection on why these meetups matter. One speaker articulated it as exposure to "unknown unknowns" -- problems and approaches that others are dealing with that you would never encounter in your own work. "It opens up a whole new world of thinking."

---

*Session recorded during the AI Engineers Saturday meetup in Chiang Mai, February 28, 2026.*
