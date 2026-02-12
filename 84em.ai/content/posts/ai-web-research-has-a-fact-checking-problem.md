---
title: "AI Web Research Has a Fact-Checking Problem"
date: 2026-02-12
draft: false
slug: "ai-web-research-has-a-fact-checking-problem"
description: "Web fetch tools can return confidently wrong prices, features, and specs alongside accurate content. Here's the verification step that caught it."
tags: ["ai", "workflow", "claude-code"]
---

I was putting together a hosting comparison for a client project. The AI tool I used to fetch and summarize pricing pages reported add-on costs at roughly $3/month. When I verified against the actual page, the real prices were $20-26/month. Not even close.

The client never saw those numbers. I verify every claim AI produces before it goes anywhere near a deliverable. That's the whole point of this post: AI speeds up my research process significantly, but it does not get the final word. I do.

## What I observed

The tool got the general context right. It identified the correct product, the correct page, the correct feature categories. But the specific numbers were fabricated. A $3/month figure instead of $26/month isn't a rounding error. It's wrong in a way that looks credible because it's sitting next to accurate information.

I don't know the exact technical reason this happens. What I do know is that web fetch tools are unreliable when it comes to specific numbers: prices, plan tiers, feature availability, version compatibility, rate limits, SLA terms. The general context tends to be solid. The specifics can't be trusted.

## Where this gets dangerous

The tricky part is that most of the surrounding content is correct. The tool accurately identifies the product name, the general feature categories, the structure of the pricing page. So if you're not in the habit of verifying, you read the output, nod along because it mostly matches what you'd expect, and miss the one number that's completely wrong.

This is worse than getting nothing back. If the tool returned garbage, you'd know to verify everything. Instead, it returns mostly-right content with confidently wrong specifics scattered throughout. That's the kind of output that passes a casual review.

## How I handle it

I treat web fetch tools as discovery tools, not fact sources. They're good for finding the right pages and understanding the general landscape. But before any specific claim goes into a client deliverable, I verify it against the actual page.

In Claude Code, that means using Playwright to open the source page and read the DOM directly. No summarization layer, no approximation. The actual content that's rendered in the browser.

The process:

1. Use web fetch for initial research and page discovery
2. Identify every specific claim that will end up in the deliverable: prices, features, version numbers, limits
3. Open each source page with a browser tool and confirm the numbers against the real DOM
4. Flag anything that can't be browser-verified as "unverified: confirm before publishing"

This adds time. It's still faster than doing all the research manually. The AI handles the discovery and general context. I handle the verification. That division of labor is what makes the workflow worth using.

## When it matters and when it doesn't

This isn't about verifying everything you ever read through an AI tool. If you're doing background research or trying to understand a topic, summarized content is fine. You're building mental context, not publishing specifics.

It matters when the output goes somewhere: a client document, a comparison table, a proposal with pricing, a technical spec with version requirements. Anywhere a wrong number changes a decision.

The rule is simple. If it's going into a deliverable, verify it. If it's informing your thinking, the summary is probably good enough.
