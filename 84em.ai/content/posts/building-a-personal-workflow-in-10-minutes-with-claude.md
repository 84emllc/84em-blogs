---
title: "Building a Personal Workflow in 10 Minutes with Claude"
slug: "building-a-personal-workflow-in-10-minutes-with-claude"
date: 2026-01-12
description: "How a morning voice dump into Google Calendar became a reusable AI-powered task management workflow."
tags: ["ai", "claude", "workflow", "automation", "productivity"]
---

This morning I dropped the dogs off at daycare around 7am. On the drive, I used Android Auto to dump ideas and tasks into Google Calendar. By the time I got home, I had about 27 calendar events with voice-transcribed titles like "follow up on staging site migration API keys" and "send invoice for plugin work last month also check on hosting renewal."

I opened Claude, asked it to fetch my calendar events for the day, and turn them into a markdown checklist organized by Morning, Afternoon, and Evening. Thirty seconds later I had a clean task list.

Then I thought: I do this regularly. Why not make it reusable?

## From One-Off to Workflow

I asked Claude to turn what we'd just done into a reusable prompt. The requirements were simple:

- Support "today" (organized by time of day) and "this week" (flat list by day)
- Fetch all events, paginating if needed
- Clean up voice transcription artifacts
- Output as markdown with checkboxes
- Provide a download link

Claude generated a prompt I can paste into any conversation, add to a Project's instructions, or save in my User Preferences for quick access.

Now I can say "calendar to tasks today" and get a formatted task list without explaining the format every time.

## The Meta Layer

This is the part that's easy to miss. The value isn't just in the task list. It's in the speed of going from "I do this manually" to "I have a tool that does this."

Traditional automation requires choosing a platform, learning its syntax, debugging edge cases, and maintaining it over time. This took a conversation. The "code" is plain English. If I want to change the format, I edit the prompt.

I'm not saying this replaces proper automation for complex workflows. But for personal productivity tools that only I use, the cost-benefit math is different. Ten minutes of conversation beats an afternoon of setting up Zapier integrations.

## What Made This Work

A few things came together:

**Voice capture is frictionless.** Android Auto lets me add calendar events while driving. The transcription is imperfect but good enough. I don't have to remember anything until I'm back at my desk.

**Claude has calendar access.** The Google Calendar integration in Claude.ai means I can fetch events without copying and pasting or exporting files. The AI can see my actual data.

**Plain language is the interface.** I didn't write code or configure settings. I described what I wanted, iterated on the output, and saved the result.

**Reusability is a conversation away.** Once something works, asking "turn this into a reusable prompt" captures the pattern for next time.

## The Prompt

For anyone who wants to try this, here's the short version to add to Claude.ai User Preferences:

> When I say "calendar to tasks" followed by "today" or "this week", fetch my Google Calendar events and create a markdown checklist. For today: organize into Morning/Afternoon/Evening sections. For this week: organize by day with flat lists. Omit times. Clean up voice-transcribed titles. Provide a download link.

You'll need Google Calendar connected in Claude.ai settings.

## The Bigger Picture

I use AI for everything from quick research questions to building enterprise applications. But this middle layer of personal utilities is where the friction used to be highest. Small automations weren't worth the setup time. Now they're a conversation away.

If you find yourself doing the same thing repeatedly in Claude, ask it to turn the pattern into a reusable prompt. You might be surprised how quickly a conversation becomes a workflow.
