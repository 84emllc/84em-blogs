---
title: "Optimizing Since 1995"
date: 2026-01-07
description: "Performance optimization lessons from three decades of web development, starting with dial-up modems and static HTML."
tags: ["performance", "wordpress", "optimization"]
---

My first real optimization project didn't involve caching plugins, CDNs, or Core Web Vitals. It involved deleting an entire CMS.

A client had a content management system that generated pages full of bloated, invalid markup. This was 1995—dial-up modems, where every unnecessary tag meant more time watching a page load line by line. The site had maybe 20 pages of content that changed once a quarter.

The fix? I rebuilt it as a static HTML site. Hand-coded pages, clean valid markup, nothing wasted. On a 28.8k modem, the difference was obvious. The client could still update content—they just emailed me the changes.

The lesson stuck with me.

## The Pattern Repeats

Thirty years later, I still see the same fundamental problem: solutions that outgrew the problems they were meant to solve. A 50-plugin WordPress install for a 10-page brochure site. Custom post types and Advanced Custom Fields for content that could live in a single page. Frameworks on top of frameworks on top of frameworks.

Sometimes the fastest optimization is subtraction.

## What Actually Matters

Most performance work I do now falls into a few categories:

**Database queries that got out of hand.** Plugins that run dozens of queries per page load. Custom code that forgot about caching. The fix is usually straightforward once you find the bottleneck.

**Hosting that doesn't match the workload.** Cheap shared hosting for high-traffic sites. Expensive managed hosting for sites that get 200 visitors a month. Right-sizing saves money and improves performance.

**Assets that nobody audited.** Fonts loading from three different sources. JavaScript libraries included twice. Images uploaded straight from a phone camera at 4000 pixels wide.

**Code that prioritized cleverness over clarity.** Abstractions that made sense to the original developer but add overhead for every request. Sometimes the boring solution is the fast solution.

## The Tools Changed, the Thinking Didn't

I use different tools now than I did in 1995. Query Monitor instead of print statements. Browser DevTools instead of View Source. New Relic and Sentry for tracking down production issues. CDNs like Cloudflare that handle edge caching and security. Sometimes a caching plugin is the right answer, sometimes manual optimization is better—depends on the problem.

But the core approach is the same: find what's slow, understand why it's slow, fix it or remove it. Measure before and after. Don't add complexity unless it solves a real problem.

The bloated CMS from 1995 taught me that. Every slow site since then has reinforced it.

---

*Need help finding what's slowing down your WordPress site? [Get in touch](https://84em.com/contact/).*
