# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of detailed abridgments from the AI community meetups in Chiang Mai, Thailand. No code. All content is markdown. Only abridgments are published; audio recordings and raw transcripts are not included for privacy reasons.

## Series and schedule

- **AI Engineers** — Saturday (technical deep-dives)
- **AI Business** — Wednesday (business strategy)
- **Agents in the Wild** — Friday (agentic AI tracking)

## Session file conventions

Files live in `sessions/` named `YYYY-MM-DD-series.md` (e.g. `2026-03-28-ai-engineers.md`).

YAML frontmatter:

```yaml
---
date: 2026-03-28
series: AI Engineers
venue: The Kannas, Chiang Mai
duration: 2h 1m
speakers: 5
youtube: https://youtube.com/watch?v=...
---
```

Only `date`, `series`, and `venue` are required. Other fields are optional.

Body format: `# Series Name — Month Day, Year` title, optional overview paragraph, then `##` sections for each major topic. Use `---` horizontal rules between sections. Include specific quotes, tool names, and participant insights. These are dense abridgments, not lossy summaries.

## Venue lookup

The Venues section in README.md has GPS coordinates for all venues. When determining venue for a new session, match against these coordinates (within 200m). The venue transitioned from 4Seas to The Kannas around Feb 2026.

## README maintenance

The session table in README.md is reverse chronological (newest first). When adding a new session, insert it at the top of the table. Each row has: date link, day of week (Sat/Wed/Fri), series name, and a short highlights summary.

## Adding a new session

1. Obtain audio from a recording, YouTube (tools like `yt-dlp` can extract audio), or an AI wearable device like Omi that continuously records and transcribes conversations
2. Transcribe with a service that supports speaker diarization (e.g. Deepgram, Whisper, AssemblyAI). Note that wearable devices like Omi may split a single meetup into multiple conversations that need to be combined chronologically
3. Write the abridgment in `sessions/YYYY-MM-DD-series.md` with frontmatter
4. Verify the day of week matches the series (Saturday=AI Engineers, Wednesday=AI Business, Friday=Agents in the Wild)
5. Add the session to the top of the README table

## Enriching existing sessions

Some sessions were written from high-level summaries and could be improved with full transcript data. If you have access to a recording or transcript for an existing session, rewrite the abridgment to match the depth and specificity of the more detailed sessions in this repo (look at any March 2026 session for reference).
