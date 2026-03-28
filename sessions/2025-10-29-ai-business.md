---
date: 2025-10-29
series: AI Business
session: 1
venue: 4Seas, Chiang Mai
duration: ~1h 30m
speakers: 7+
---

# AI Business — October 29, 2025

First session of the AI Business series at Darkstar HQ. A mixed group — some building AI products, some running traditional businesses looking to integrate AI, and a few exploring where the opportunities are. The session was structured as an open roundtable, with each participant sharing where they are and the group workshopping ideas in real time.

---

## 1. Roundtable: Where Is Everyone At?

The host opened by polling the room. Most attendees were either in early stages of an AI business or running an existing business trying to figure out where AI fits. Backgrounds ranged from lead generation and digital marketing to consulting, open-source tooling, and disability services in Australia.

One participant runs a lead generation business for home improvements and legal claims in the UK — builds websites, runs Google Ads, and feeds leads to clients like law firms. He described his setup as largely self-sustaining: "For the last four or five months I haven't really had to do very much, which is why I just do the Google Ads." He only runs search campaigns, avoids Facebook because "you deal with a lot less complaints when you do Google Ads because you're further down the funnel."

Another attendee works in design — generating graphics with specific vector-based styles for commercial use. The group discussed his workflow in detail: the problem breaks down into three steps (generate an image, produce suitable text, arrange it with the right font and positioning), each of which can be done with AI individually but automating the full pipeline is the challenge. Flux was suggested for fine-tuning on 50-60 reference designs to train a consistent style, and the group noted that most generators "tend to fall to the same design patterns even if they're creating vector files" — custom training would be needed for his niche.

A third participant builds with Ruby — an open-source CLI tool that unifies WiFi management commands across Mac, Ubuntu, and Linux. "Very few open source tools have any kind of multimedia introduction. It's usually just a readme." He was looking for advice on creating a short promotional video.

---

## 2. Models, Agents, and Tools — The Building Blocks

The host gave a concise breakdown of the AI stack for the less technical attendees:

- **The model** is the brain — "all of the connection points that basically give you the next token, that give you the piece of text, image, whatever."
- **The agent** is a transformer between the user and the model. It prepares the user's input, sends it to the model, and formats the response. "If you are talking in natural language through the ChatGPT interface, the response is going to be text. It won't be a massive JSON file if you're asking 'hello, how are you?' — that's the agent's job."
- **Tools** are how agents connect to the outside world — APIs, MCPs (Model Context Protocols). "If you have problems with Supabase, you need something to connect your language to Supabase."

The key takeaway: "The brain behind, you have to disassociate it from the tool that you're using." The best approach for someone starting out is to pick the agent best equipped for their workflow, and when it comes to models, the choice matters less than the interface layer.

For one attendee who was clearly finding the discussion abstract, the host suggested a practical approach: "Rather than talking about it abstractly, maybe sit down with someone that already uses these tools and show you how we use them. I think it becomes more understandable."

---

## 3. The Arbitrage Window

The conversation turned to the central question: what are the business opportunities right now that won't exist in six months?

One participant shared an anecdote about an entrepreneur from Hong Kong who was building a video tool. When told Sora 2 would make it obsolete, his response: "I'll make a million dollars in those six months." The group agreed this captures the current moment — speed is the moat. "Too many people are still doing three and six month builds, which I think is gonna lose them speed or momentum."

The host framed the opportunity tiers:

1. **Simple automation for small businesses** — answering customer inquiries, managing schedules, bookings, price information, stock management. "Every business needs customer service to some extent. This is all very easy to automate." But the room acknowledged this is now saturated: "Just go on Reddit and you will find people that build your workflows for free or for $20."

2. **AI consulting on internal data** — the high-value play. The host shared a case study from his own work: "The company I'm working for, we're digitalising all their business processes. They found out they actually have customers they're losing money on." A 40-year IT company discovered that a big-name client like Siemens "don't buy a lot of shit from us — they just want quotations, maybe bought a few services, but open a shitload of support tickets, always want the sales guy there once a month for a nice lunch. We actually lose money on them." Before AI analysis of their ERP data, they never saw it.

3. **Hardware + domain expertise** — combining always-on listening devices or niche hardware with AI software. The moat comes from the physical product, not the code on top.

4. **Faceless video and marketing content** — still viable for short-form content at scale, but taste and creative direction are becoming the differentiator, not tool access.

---

## 4. Google Ads and AI — A Practitioner's View

The lead generation specialist gave a grounded take on how AI is already embedded in Google Ads. He participated in a Google pilot scheme where a Google technician optimised campaigns for free, working off Google's AI-generated recommendation scores.

His verdict: "It's basically just making the whole process more efficient by offering suggestions and automation throughout ad creation. It's not like you can go in and say 'make me Google Ads' and it makes you perfect ads. You need the knowledge to apply the suggestions." Without domain expertise, "someone would just end up with a load of headlines that just weren't very good."

On whether AI overviews in search results have hurt his traffic: "I haven't really seen that too much" — his verticals are seasonal and he saw no clear correlation with AI feature rollouts.

The group discussed building an AI wrapper for Google Ads — a ChatGPT-style interface connected to the Google Ads API that generates text, images, titles, and places campaigns automatically. The specialist agreed it could work but noted keyword research remains the real workload.

---

## 5. The Value of Existing Data

A recurring theme: businesses sitting on years of data don't realise its value.

The host argued that the lead generation specialist's archive of thousands of campaigns is an untapped asset: "Throw AI at this and ask, what is the pattern here? Why are these better than the other ones? It maybe sees some consistencies — these campaigns had a few things in common while the very bad performing ones had these kind of things in common."

One participant brought up Hotjar as an example of a company with extraordinary data: "They record the whole interaction on your website. They must have so much data on how to absolutely refine conversion to the max."

Another mentioned Precision, a tool for building dashboards from internal data — "especially when you look at lead generation, you've got click-through rate, conversion rate, all of that. You can make some really nice dashboards for marketing companies."

The host confirmed this is an up-and-coming market, especially for consultancies: "You come to a business and either start annotating their data, provide analysis, or provide automation using tools like n8n. It's a hard market because it relies mostly on your connections in the B2B space — distribution becomes the key."

---

## 6. Where Is the Money for Non-Technical Businesses?

One participant pushed back on the technical focus: "I came for a business meetup. Where can we make something that is actually gonna be profitable?" He raised the example of a hairdresser using AI to suggest haircuts — niche but addressing a massive market.

The host's response: "My first thought wouldn't be 'I use AI for the haircut' — I'd jump on automating the underlying administrative bullshit that no one wants to deal with." But he acknowledged the saturation problem: "Everyone does that now."

The deeper point: "Every service is very easy to copy. But the moat isn't necessarily about creating the best solution — it's about building your lock-in." Whether that's ease of use, onboarding, long contracts, or a piece of hardware — "it stems from your domain expertise."

A participant shared how he coaches a business consultant: the consultant went to ChatGPT, described his skills, and asked "who in the world needs this and has disposable income?" He came back with a target list of 150 prospects. "Some of these people, like investment bankers, either don't need your service or might have their money locked up" — but the approach of using AI for market discovery impressed the room.

---

## 7. Hardware and Domain Expertise — The Omi Device and Incident Reporting

One of the more detailed case studies came from a participant building for Australian disability services. Frontline workers supporting people with disabilities are legally required to write incident reports, but "half these people, English is not a primary language. They don't know how to write it properly. They don't know how to ask the appropriate questions."

His solution: a voice app. "Just say 'state before events happen,' and then a whole lot of questions and answers get generated for you." The system walks through what happened before, during, and after an incident, then runs micro-prompts for analysis — "is it incompetence? Is it preventable? Could you train the client?"

His technical philosophy: "Too many prompts is not a problem. Single responsibility principle. The more you can do fine-tuned questions or answers or transformations — don't ask a question and transform it into markdown. Ask your question, get your data. In another prompt, turn it into markdown." He called this context engineering.

He also demonstrated the Omi device — an always-on listening wearable used during the meetup itself to capture the full transcript. Key features:

- Speaker diarisation — identifies different speakers and, if names are mentioned, labels them
- Tonality analysis — "It'll say it sounds like you were in a group meetup discussing technology. The mood was exciting."
- Memory integration — transcripts are passed into a persistent knowledge base. "I can look up all our conversations from Wednesday and Saturday meetings and say 'we were talking about this thing' — it'll pull that forward, dig through the transcript."
- Fully open source — both software and hardware. "Even the hardware is open source, so you can build it yourself at home if you know how to solder." Three-D printed versions exist using Arduino hardware.

The host highlighted this as a template: "If you can find what people are lacking in their day-to-day and find a business that would drive value from that, the software on top is kind of irrelevant because you need that specific piece of hardware tied to your software."

---

## 8. AI Video Generation — Sora 2, Hygen, and the Creative Frontier

The final stretch covered video generation tools for marketing:

**Sora 2 Pro** was the standout. Its new storyboard feature allows chaining 5, 10, or 25-second clips together with consistent characters — "I did one where I had a main character and it kept that character's consistency all the way through without having to upload it as an avatar. That actually surprised me." However, it's US-only (VPN works on the web version but "it is super slow" and "the website's awful"). One participant managed to generate up to 9 clips in a single storyboard.

The group's consensus: Sora 2 leads for realistic video because of its real-world physics understanding. "Genuinely surprised it could understand the world as it went into the water — everything magnified." Kling 3.1 was noted as decent but a step behind.

**Hygen** was praised for avatar-based tutorials: "We create the app, use a little bit of LLMs to create the scripts, and once the client's happy, we just create 50." The avatar generation is fast, and outputs are good quality.

**For budget workflows** (image-to-video rather than text-to-video): Leonardo, DALL-E, and Midjourney for image generation, then animation tools on top. A 15-second video breaks into three 5-second scenes, with standard generation at 7-8 seconds per clip.

The creative argument: "It comes down to taste. The people with taste will be able to create more emotion, more feel." One participant is funded by a US-based client on a monthly retainer specifically for artistic AI videos — "our philosophy is it doesn't matter how many videos we get out. It's the art. Can we think of it the way George Lucas would look at filmmaking?"

**Practical tip for beginners:** CapCut's free green screen feature — record yourself, press remove background, layer over a screencast. "Go onto YouTube and search 'green screen CapCut' — you'll see how easy it is."

---

## 9. Wrap-Up and Logistics

The host announced:
- Next session in two weeks, moving venue to 4Seas (same building as the Saturday meetups, third floor, inside the glass doors)
- A centralised tool repository is in progress — every tool mentioned in sessions will be catalogued with short summaries and open for community comments
- A WhatsApp group exists for between-session discussion

*Session recorded at the AI Business meetup, Darkstar HQ, Chiang Mai, October 29, 2025.*
