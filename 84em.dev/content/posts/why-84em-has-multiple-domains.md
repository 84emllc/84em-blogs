---
title: "Why 84EM Has Multiple Domains Now"
slug: "why-84em-has-multiple-domains"
date: 2026-02-19
description: "How splitting services and content across 84em.com, .io, .dev, and .ai gives each audience a dedicated front door instead of one crowded homepage."
tags: ["business", "hugo", "static-sites", "ai", "workflow", "infrastructure"]
---

I've been building for the web for 31 years. For the last 14, 84EM has been the vehicle: custom development, agency partnerships, and WordPress work across industries. That positioning served me well, but over the past year the work changed and the brand needed to catch up.

## The Problem With One Domain

More clients started coming to me with the same story: a previous vendor couldn't deliver, the project stalled, and now they need someone to pick it up and ship it. Sometimes it's WordPress. Sometimes it's React, Next.js, Python, or an AI integration that got halfway built and abandoned.

Project rescue is already a service on 84em.com. But the volume and variety of these requests convinced me it deserved its own front door -- a dedicated domain with focused messaging instead of a section buried in a larger service catalog.

## The Domain Strategy

Rather than cramming everything onto 84em.com, I split services and blogs across multiple domains:

- **84em.com**: The corporate site. Custom development, AI integrations, agency partnerships, and the full service catalog I've built since 84EM's inception.
- **84em.io**: Project rescue and AI integration. The new service line.
- **84em.dev:** The development blog. Technical writing, walkthroughs, and notes from the shop floor.
- **84em.ai:** The AI blog. Tools, workflows, and what holds up in real projects.

Each domain serves a distinct audience. Development help lands on .com, stalled builds on .io, technical deep dives on .dev, and AI tools and workflows on .ai.

## Building .IO With Claude Code

The .io site is a Hugo static site built with a multi-tool AI workflow:

- I started with Gemini to spitball ideas around the theme and positioning
- Distilled that into a master system prompt defining the design system, layout structure, and content philosophy
- Claude Code wrote every layout and line of CSS from scratch
- I used custom Claude Code agents to run SEO and accessibility audits and remediate issues in the same workflow

A few details worth noting:

**Custom Hugo theme.** Hugo compiles to static HTML with no server-side runtime, which means fast load times and minimal attack surface. I built a custom theme from scratch.

**CSS-only animations.** The hero section has a breathing grid animation, the diagnostic terminal has a typing reveal effect, and the service cards use glassmorphism. All pure CSS with custom properties. No JavaScript animation libraries.

**Accessibility-first.** Every text color meets WCAG 2.2 AA contrast ratios against the dark background. The design system includes dedicated AA-compliant variants of the brand orange and green specifically for text use. A `prefers-reduced-motion` media query disables all animations for users who need it.

## Why This Matters

The market for AI-assisted development is moving fast, and a lot of projects are getting started by teams without the engineering depth to finish them. That creates a growing need for experienced developers who can step in, assess the damage, and deliver.

That's the work .io is built to attract. A dedicated domain with focused messaging, built using the same tools and workflows I bring to client projects.

If you have a stalled project or an AI integration that needs to ship, [start a conversation ↗](https://84em.io/#contact).
