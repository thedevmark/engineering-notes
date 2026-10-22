# Build notes: editorial record

## Purpose

Explain decisions inside Mark's games and tools to people deciding whether to use the work, collaborate, or hire him. A reader should understand the problem before encountering implementation terms.

## Selection and voice

On 22 October 2026, Mark asked for executive decisions about papers that felt inflated and unrepresentative. Lead with Chat vs. Meteors, the video upload work, and Pathos. Keep narrower infrastructure and bot notes available after those stories.

Write in a direct first-person voice when the source supports Mark's own work or recorded observations. Do not invent a personal anecdote, thought process, measurement, or reaction. Start from a real constraint, explain the decision, and retain the limitation that changes its meaning.

Examples:
- “A desktop viewer and a phone viewer can be responding to different moments in the same round.” — chat-vs-meteors/README.md
- “A green check in an extension was evidence that the extension ran, not that the platform delivered 60 fps.” — 4k60-native-ingest/README.md

Preserve the exact name 4K60 Native Ingest and existing article paths. Use diagrams only where they explain the decision. Do not restore paper/stack tables, speculative audience-scale charts, or the repeated app catalog.

## Evidence boundaries

The source check for this revision establishes implementation behavior, not a new gameplay study, load test, phone test, or production deployment. The video route findings remain the author's September observations. Public implementation links are used where the source is public; private repositories are not presented as reader-accessible evidence.

The profile README in thedevmark/thedevmark owns the project catalog. This repository owns the build notes. Keep each fact at its useful location instead of duplicating that catalog here.
