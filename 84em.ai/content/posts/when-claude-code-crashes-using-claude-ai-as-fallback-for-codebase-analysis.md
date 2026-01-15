---
title: "When Claude Code Crashes: Using Claude.ai as a Fallback for Codebase Analysis"
slug: "when-claude-code-crashes-using-claude-ai-as-fallback-for-codebase-analysis"
date: 2026-01-15
description: "How to work around Claude Code memory limits by offloading large codebase analysis to Claude.ai and generating execution prompts for Claude Code."
tags: ["claude", "claude-code", "workflow", "debugging", "ai"]
---

Claude Code is my go-to for working inside codebases. It reads files, runs commands, and executes changes in context. But it has limits.

This morning I was working on a WordPress plugin refactor. Version 3.0 moved from local database validation to HubSpot API calls, and I needed to find all the dead code left over from v2: unused database methods, orphaned admin screens, legacy partials, and a composer dependency that was no longer needed.

I asked Claude Code to scan the codebase and identify what could be removed.

It crashed.

```
FATAL ERROR: Ineffective mark-compacts near heap limit
Allocation failed - JavaScript heap out of memory
```

## The Workaround

Instead of fighting with memory limits or trying to chunk the analysis, I zipped the project directory and uploaded it to Claude.ai.

Claude.ai doesn't have the same execution capabilities as Claude Code. It can't run `git status` or execute `composer update`. But it can read and analyze files just fine.

I asked the same question: scan for legacy v2 remnants and dead code.

Within a few minutes, I had a complete analysis:

- 5 files to delete entirely
- 4 files needing specific modifications
- Line numbers and code blocks showing exactly what to remove
- Verification commands to confirm the cleanup worked

## The Handoff

Here's where it gets useful. I asked Claude.ai to generate a detailed prompt I could paste back into Claude Code.

The output was a structured task list in markdown: files to delete, specific edits with before/after code blocks, composer.json changes, and a commit message. Everything Claude Code needed to execute the cleanup without having to re-analyze anything.

I pasted that prompt into Claude Code. It ran through the task list, made the changes, and the job was done.

## Why This Works

Claude Code is built for execution—it navigates directories, runs commands, and makes changes iteratively. Claude.ai is better for comprehensive analysis because it loads everything at once and analyzes it in a single pass, without the complexity of maintaining filesystem state. For pure analysis tasks—finding patterns, identifying dead code, reviewing architecture—Claude.ai's simpler nature is an advantage.

The crash I hit was specific to Claude Code trying to maintain and analyze a large codebase through sequential commands. Claude.ai sidesteps that by processing everything upfront.

Splitting the work plays to each tool's strengths:

1. **Claude.ai** for analysis and planning
2. **Claude Code** for execution

## The Actual Prompt

For reference, this is the structure I asked Claude.ai to generate:

- Section listing files to delete with reasons
- Section listing files to modify with exact code changes
- Verification steps (grep commands to confirm cleanup)
- Pre-written commit message

Claude Code consumed that prompt and executed it without issues. No memory crash, no confusion about scope.

## When to Use This Approach

This isn't my default workflow. Most tasks fit fine in Claude Code. But when you're doing broad codebase analysis, looking for patterns across many files, or asking questions that require loading a lot of context at once, the memory limits become real.

Signs you might need the fallback:

- Claude Code crashes or becomes unresponsive during analysis
- You're asking about patterns across a large codebase
- The task is more about "find and report" than "find and fix"

The zip-upload approach adds a step, but it's faster than fighting with a crashed session or trying to manually chunk the analysis.

## Tools Used

- **Claude Code** (Anthropic's CLI tool for agentic coding)
- **Claude.ai** (web interface, same underlying model)
- A zip file of the project directory

Nothing fancy. Just knowing which tool handles which part of the job.
