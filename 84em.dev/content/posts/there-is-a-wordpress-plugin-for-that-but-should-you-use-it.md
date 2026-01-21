---
title: "There's a WordPress Plugin for That (But Should You Use It?)"
date: 2026-01-21
description: "How to evaluate WordPress plugins when the wrong choice costs months of work."
tags: ["wordpress", "plugins", "security", "development"]
---

A client asked me to build a credit application form in WordPress. They wanted to collect social security numbers, employment history, income verification—everything a lender needs to process a loan.

Plugins exist that could do this. I recommended a third-party service instead.

Not because WordPress can't handle sensitive data. It can. But the liability of storing social security numbers and financial data on their WordPress site wasn't worth avoiding the integration work with a service built for that level of security.

If the client had insisted on WordPress for credit applications, I would have turned down the work.

That's an extreme case. Most plugin decisions aren't about whether to use WordPress at all. They're about which plugin to use when dozens claim to solve the same problem.

Every client site I build uses third-party plugins. I don't reinvent contact forms or caching or SEO tools when trusted solutions already exist. But "there's a plugin for that" is where the evaluation starts, not where it ends.

## The Hidden Cost of the Wrong Plugin

I built an enterprise site that used a popular forms plugin. At launch, it had everything you look for: years of active development, responsive support, regular updates, thousands of installs. I did the evaluation. The plugin was solid.

Mid-project, the authors abandoned it.

I maintained that site for over four years after launch. No updates from the original developers. Compatibility issues with newer PHP versions. Performance problems on high-traffic pages. I had to patch it myself.

Replacing it meant rebuilding dozens of complex forms with conditional logic, payment processing, and CRM integrations. The math worked out: cheaper to maintain someone else's abandoned code than to start from scratch. But it was tedious maintenance work that shouldn't have existed.

That's the risk you can't fully control. You can evaluate a plugin perfectly and still end up maintaining abandoned code when the authors move on.

## How I Evaluate Plugins

I look at code first. A quick scan tells you most of what matters.

Prepared statements for database queries. Nonces on form submissions. Capability checks before privileged operations. These are a few examples of WordPress security basics. If a plugin skips them, that's a signal about the developer's competence or care.

Security history matters more than a clean record. Everyone makes mistakes. Reputable companies fix them fast and don't repeat the same errors. A plugin with one serious vulnerability that got patched in 48 hours tells me more than a plugin with no reported issues but only 200 installs.

Install count is a signal, not a guarantee. A million installs means thousands of developers and security researchers have looked at the code. Vulnerabilities get found and reported. At 100 installs on a brand new plugin, you're the beta tester.

Maintenance track record beats current status. A plugin actively maintained for five years is a better bet than one with six months of frantic updates followed by silence. Regular releases that address WordPress core changes show commitment. Radio silence for a year shows abandonment.

## What Agencies & Developers Get Wrong

Some folks treat plugins like grocery shopping. Need a feature? Install a plugin. Site gets slower? Install a caching plugin. Security concern? Install a security plugin.

I've seen client sites with over 90 plugins. Lots of conflicts with each other. Some doing duplicate work. Heck, I once inherited a site once that used 3 separate page builder plugins. All of them adding weight to every page load on the front end. Slowing things down dramatically in the admin.

The issue isn't always competence. Smaller agencies often don't have a backend developer who knows what to look for. Some developers are junior and don't know what to look for either. And some aren't truly developers, they're customizers: install a plugin, tweak settings, call it done. Never write complex code. They're doing their best with the information available: high ratings, lots of installs, positive reviews. Those matter, but they're not enough.

## The Plugins I Trust

So what do trusted plugins actually look like? I wrote a [previous blog post](/posts/the-wordpress-plugins-i-actually-use/) about the ones I use on client sites.

## WordPress Core Is Secure

The plugin ecosystem gets attention because it's variable. WordPress itself has a strong security track record. The core team takes security seriously. Automatic updates for critical patches. A dedicated security team. A responsible disclosure process.

The risk isn't WordPress. It's choosing poorly from 60,000 plugins in the repository.

## The Real Question

"There's a plugin for that" isn't helpful by itself. The useful questions are: Who wrote it? How long have they maintained it? What happens if they stop? Does this belong in WordPress at all?

Sometimes the answer is a trusted plugin. Sometimes it's custom development. Sometimes it's a third-party service built for the job.

The difference between those options is judgment, not just technical capability. That's what 30 years of writing code teaches you: not just what's possible, but what's sustainable.
