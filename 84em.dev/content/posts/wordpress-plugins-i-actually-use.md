---
title: "The WordPress Plugins I Actually Use"
date: 2026-01-20
description: "Eight plugins that solve real problems in client work, from email reliability to search performance."
tags: ["wordpress", "plugins", "tools", "recommendations"]
---

Since I started specializing in WordPress development in 2012, I've installed, tried and tested hundreds of plugins. Most get uninstalled within a week. These nine stay.

## FluentSMTP

WordPress's `wp_mail()` function is unreliable. Shared hosting providers throttle outbound email. Messages land in spam folders or don't send at all.

[FluentSMTP ↗](https://fluentsmtp.com/) routes email through actual mail services: SendGrid, Mailgun, Amazon SES, or any SMTP server you control. Configure it once, forget about it. Email logging shows exactly what was sent and when, which matters when a client asks "did that password reset email go out?"

Bonus points for the ability to configure multiple email services with fallback redundancy. I use my Google Workspace email as my primary and Brevo's free plan for my backup. 

## Relevanssi

WordPress's built-in search is a database query against post titles and content. It doesn't understand synonyms. It can't weight results by relevance. It breaks on large sites.

[Relevanssi ↗](https://www.relevanssi.com/) replaces it with actual search indexing. Results rank by relevance instead of chronological order. It handles partial matches, custom fields, and taxonomy terms. Configuration lets you boost specific post types or exclude others entirely.

For sites with hundreds or thousands of posts, the difference is visible immediately. Users find what they're looking for instead of giving up and using Google.

## Gravity Forms

Contact forms shouldn't be complicated, but most form plugins make them that way.

[Gravity Forms ↗](https://www.gravityforms.com/) handles everything from simple contact forms to multi-page applications with conditional logic, file uploads, and payment processing. The conditional fields feature alone justifies the cost: show or hide form sections based on previous answers without writing JavaScript.

API integration is straightforward. I've connected forms to HubSpot, Salesforce, custom REST endpoints, and internal databases. The webhook add-on handles most cases without custom code.

Developer-friendly: clean markup, [documented hooks ↗](https://docs.gravityforms.com/), and a PHP API that makes programmatic form manipulation possible. I can build a form in code if the visual builder isn't the right fit.

## FlyingPress

Performance optimization is tedious. Minify CSS. Defer JavaScript. Lazy load images. Optimize fonts. Add caching headers. Enable compression.

[FlyingPress ↗](https://flyingpress.com/) does all of it through a UI that actually makes sense. Turn on the features you want, leave off the ones that break your site. The critical CSS generation works better than manual attempts, and the JavaScript delay feature speeds up sites without breaking functionality.

I've tested it against WP Rocket, Autoptimize, and manual optimization. FlyingPress consistently produces better Lighthouse scores with less configuration.

## Two-Factor

Username and password authentication stopped being sufficient years ago.

[Two-Factor ↗](https://wordpress.org/plugins/two-factor/) adds multiple authentication methods to WordPress: TOTP codes via authenticator apps, email codes, FIDO U2F hardware keys, and backup codes. Users can enable one or several. Login requires both password and a second factor. Simple, effective, widely understood.

I enable it for all admin accounts on client sites. It's prevented account takeovers on sites with compromised credentials. The extra ten seconds at login is worth avoiding the hours of cleanup after a breach.

## Wordfence

Not every site needs a security plugin. A simple brochure site with regular updates and strong passwords faces minimal risk. But for clients whose WordPress site is mission-critical to the business, security moves up the priority list.

[Wordfence ↗](https://wordpress.org/plugins/wordfence/) provides endpoint firewall protection, malware scanning, and brute force login prevention. The scanner compares core files, themes, and plugins against the WordPress.org repository and flags modifications. When something gets compromised, it can overwrite infected files with clean versions. For clients who need extra security, I recommend the paid version: it gets malware signature updates in real-time instead of the 30-day delay on free.

For high-value sites, I pair Wordfence with [Cloudflare's WAF ↗](https://www.cloudflare.com/application-services/products/waf/). Wordfence catches WordPress-specific threats at the application level. Cloudflare blocks attacks at the edge before they reach the server. Defense in depth.

## Simple History

When something breaks on a client site, the first question is always "what changed?" Without an audit log, you're guessing.

[Simple History ↗](https://simple-history.com/) tracks user activity automatically: post edits, plugin updates, theme changes, media uploads, login attempts, settings modifications. No configuration required. Install it and it starts logging.

The search and filter tools make it easy to find specific events. When a client says "the site looked different yesterday," I can see exactly who changed what and when. On multi-user sites, it adds accountability. On single-user sites, it still catches the "I don't remember changing that" moments.

Developer-friendly: WP-CLI support for viewing logs, JSON output, and an extensible API for custom logging in themes and plugins.

## WP Migrate

Moving WordPress sites between servers should be simple. Export database, copy files, import database, update URLs. In practice: serialized data breaks, file permissions fail, database imports time out on shared hosting.

[WP Migrate ↗](https://deliciousbrains.com/wp-migrate-db-pro/) handles it. Push or pull the entire database or select specific tables. Migrate all plugins or choose individual ones, same for MU plugins and themes. Search and replace handles serialized data correctly. Media library sync moves only the files that changed.

The free version covers basic migrations. The paid version adds media library sync and multisite support. I use it weekly for staging-to-production deployments and client site migrations.

Developer-friendly: full WP-CLI integration for running migrations, importing database dumps, and executing saved profiles from the command line.

For developers comfortable with the command line: SSH and rsync remain viable alternatives for file transfers, especially on servers where direct plugin connections aren't possible. WP Migrate isn't my only tool, but it's the one that saves the most time when both environments support it.

## Cloudflare Turnstile

CAPTCHA challenges are annoying. Spam form submissions are more annoying.

[Cloudflare Turnstile ↗](https://www.cloudflare.com/application-services/products/turnstile/) is Cloudflare's reCAPTCHA replacement. Most visitors never see a challenge. When needed, it's a single click instead of identifying crosswalks in twelve separate images. Integration is a [plugin install ↗](https://wordpress.org/plugins/simple-cloudflare-turnstile/) and an API key paste.

Spam submissions dropped to near zero on sites using it. False positives are rare. The user experience is significantly better than traditional CAPTCHA.

## Why These Plugins

I don't install plugins because they're popular or free. I install them because they solve problems I encounter repeatedly in client work.

Email needs to be reliable. Search needs to work. Forms need to collect data without breaking. Sites need to load fast. Accounts need protection. Migrations need to succeed. Spam needs to stop.

These nine handle those tasks without requiring constant maintenance or causing compatibility issues. That's what makes them worth using.
