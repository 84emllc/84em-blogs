---
title: "The Subscriptions Behind Every Client Project"
date: 2026-02-09
description: "The paid services that make client work sustainable, and why free alternatives don't cut it."
tags: ["tools", "services", "infrastructure", "business"]
---

I pay for services when the free version costs me more in time, risk, or client trust than the subscription price.

## Kinsta

Managed WordPress hosting isn't cheap. Shared hosting and VPS options cost less.

I use [Kinsta ↗](https://kinsta.com) because support actually helps instead of pointing you to documentation. Automated backups run daily. Staging environments take one click. PHP version updates are painless. CDN is built in.

When a client site goes down at 2 AM, I need it back up in minutes, not hours of troubleshooting server configuration.

Kinsta's backups live on Kinsta's infrastructure, and I trust them, but redundancy matters. [AWS S3 ↗](https://aws.amazon.com/s3/) storage is inexpensive and Kinsta can send automated backups there.

If Kinsta ever has a major failure, client sites have offsite backups that survived. Low probability. Minimal cost.

## Cloudflare (Paid Tier)

[Cloudflare's ↗](https://www.cloudflare.com) free tier handles DNS and basic DDoS protection. For a high-traffic site generating revenue, that's not enough.

I pay for Pro or Business tiers on client sites that can't afford downtime. Web Application Firewall catches attacks before they reach the server. Custom SSL certificates work with enterprise setups. Page rules let you tune caching per URL pattern.

Support responds when something breaks instead of directing you to community forums.

Paid protection is cheaper than one successful attack.

## PhpStorm

VS Code is free. [PhpStorm ↗](https://www.jetbrains.com/phpstorm/) isn't.

PhpStorm ships with WordPress support built in. It knows the hook system, understands template hierarchy, and autocompletes function parameters without chasing down extensions.

The database tools let you run queries, inspect tables, and export data without leaving the IDE. Refactoring works: rename a function and every reference updates.

The debugger connects to Xdebug without wrestling with configuration files.

VS Code can do some of this with the right extensions installed and configured. PhpStorm does it without that overhead. That's worth it.

## Sentry

Error tracking exists in hosting panels and server logs. [Sentry ↗](https://sentry.io) makes it actionable.

When a plugin throws a fatal error on one specific page for users in one browser, Sentry tells me which page, which browser version, which PHP version, and the exact line of code that failed.

I get real-time email and Slack alerts. Stack traces show the full call chain. Breadcrumbs show what the user did before the error.

Release tracking connects errors to deployments, so I know which deploy introduced the problem.

Server logs tell you something broke. Sentry tells you what, where, and why.

## GitHub

Private repos are free. [GitHub's ↗](https://github.com) paid features are where the value is.

Actions minutes run automated tests and deployments on every push. Copilot handles repetitive code patterns so I can focus on the logic that matters. Advanced security scans for vulnerabilities and secrets before they reach production.

Free-tier Actions minutes run out fast on active projects. Paid plans keep the pipeline running.

## New Relic

Sentry catches errors. [New Relic ↗](https://newrelic.com) catches performance problems.

A database query taking 4 seconds won't throw an error, but it will make pages load slowly. New Relic's transaction tracing shows exactly which query, which plugin, and which function is the bottleneck.

The service maps show external API calls that are timing out. Database analysis identifies missing indexes.

When a client says "the site feels slow," New Relic turns that into "this query needs optimization."

## Uptime Robot

The free plan of [Uptime Robot ↗](https://uptimerobot.com) checks sites every 5 minutes. Paid plans check every 60 seconds or less.

For sites where every minute of downtime costs money, that gap matters. An ecommerce site running a flash sale needs to know immediately if the site goes down. A brochure site? A 5-minute wait is fine.

The paid plan also alerts via SMS and Slack instead of just email. By the time I see an email, a client may have already noticed.

## Scribe

Writing documentation means taking screenshots, adding arrows and highlights, then writing step-by-step instructions. [Scribe ↗](https://scribehow.com) does it automatically.

Turn on the extension, perform the task, turn it off. Scribe captures every click and generates documentation with screenshots, annotations, and instructions.

For client handoffs or internal processes, it turns 30 minutes of screenshot editing into 30 seconds of review.

## Loom

Some documentation needs video. [Loom ↗](https://www.loom.com) records screen and camera, uploads automatically, and generates shareable links.

When a client asks how to use a custom admin feature, a two-minute Loom replaces a dozen annotated screenshots and a page of written instructions.

The free plan caps recordings at five minutes. That's just long enough to start explaining something complex and run out of time.

## Calendly

Email tennis for scheduling costs more time than a subscription.

[Calendly ↗](https://calendly.com) shows availability, lets clients book directly, and handles time zones automatically. The free plan limits you to one event type and one calendar.

I need multiple event types for different meeting lengths, multiple calendars synced to prevent conflicts, and custom confirmation pages after booking.

I customize every email notification and have Slack integration so I see bookings without checking another app. Removing Calendly's branding keeps my name on the page, not theirs.

Ten back-and-forth emails to find a meeting time wastes billable time. A $10/month subscription eliminates that.

## Trello

Spreadsheets and email threads lose tasks. [Trello ↗](https://trello.com) doesn't.

The free plan gives you basic boards. I need more than that. Automations move cards between lists when status changes, so I'm not manually dragging things around. The calendar view shows what's due across every project. Power-ups connect boards to the tools I already use.

Some boards are internal. Others are client-facing, giving clients visibility into progress without scheduling a status call.

The free plan caps automations and power-ups. The premium plan removes those limits.

## Slack

Email is too slow for active projects. [Slack ↗](https://slack.com) keeps conversations searchable and organized.

The free plan deletes message history after 90 days. On a long-running client project, that means losing context on decisions made months ago. The Pro plan keeps everything.

I run one workspace for all of 84EM. Client channels keep project conversations separated by account, so team discussions about one client don't bleed into another.

Integrations pipe in alerts from Sentry, Uptime Robot, Calendly, and other services so I'm not checking multiple dashboards.

## Bitwarden

[Bitwarden's ↗](https://bitwarden.com) free plan handles unlimited passwords across unlimited devices.

I pay less than $20 a year for the premium plan because it consolidates two workflows. The built-in TOTP authenticator stores two-factor codes alongside the credentials they protect. No switching between apps every time a client portal asks for a verification code.

Encrypted file storage keeps license keys, SSL certificates, and sensitive client documents in the same vault.

## The Common Thread

I don't pay for services because they're popular or because other developers use them. I pay for them because the alternative costs more.

Free error logging means manual log review. Free IDE means hunting down extensions. Free uptime monitoring means longer downtime. Free project management means lost tasks. Free team chat means lost history. Free scheduling means email tennis.

These services handle recurring problems without requiring recurring attention.