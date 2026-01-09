---
title: "AI-Assisted Content Migration: From Discovery to Deployment"
date: 2026-01-08
description: "How Claude Code handled a WordPress content update from database analysis through safe deployment, with minimal human intervention."
tags: ["ai", "wordpress", "automation", "claude-code"]
---

[84EM.COM ↗](https://84em.com) had "13 years of experience" and "30 years of programming" hardcoded across 60+ pages. Every January, I'd need to find and update these references. The task seemed straightforward until you start counting the variations: hero blocks, template files, generated local SEO pages, FAQ sections.

Rather than manually hunting through the WordPress admin, I handed the problem to Claude Code.

## Discovery: Let AI Do the Counting

The first step was understanding the scope. Claude generated and ran a database query to find all instances:

```sql
SELECT post_type, COUNT(*) as count FROM wp_posts
WHERE post_status = 'publish'
AND (post_content LIKE '%13 year%' OR post_content LIKE '%30 year%')
GROUP BY post_type;
```

Result: 63 content items across pages, reusable blocks, and templates. More than expected. The query also surfaced variations I hadn't considered - "nearly 30 years," "over 13 years," "13+ years."

This is where AI shines. I described the problem; it figured out how to measure it.

## Solution Design: AI as Architect

I explained the goal: replace hardcoded years with something that updates automatically. Claude proposed three approaches:

1. **Content filter** - Intercept content on render and replace text
2. **Shortcodes** - Store base years, calculate dynamically
3. **Custom blocks** - Gutenberg blocks with year logic

It recommended shortcodes as the simplest, most maintainable option. No magic behavior, explicit in the content, easy to debug. I agreed.

Claude then designed the shortcode API:

```
[years_since year="2012"]  → calculates years since 2012
[wp_years]                 → alias for WordPress experience
[dev_years]                → alias for programming experience
```

Clean, flexible, self-documenting.

## Implementation: Code Generation

With the design approved, Claude wrote the implementation: a PHP file with the shortcodes and a WP-CLI command class for the migration.

The migration command included something I wouldn't have thought to add: a dry-run mode.

```bash
wp 84em dynamic-years migrate --dry-run
```

This previews every change without modifying the database. Essential for a migration touching 63 pieces of content. Claude's instinct for defensive programming saved potential headaches.

## The Migration: 68 Replacements in Seconds

The dry-run showed 68 replacements across 62 items. Some pages had multiple year references. After reviewing the preview, the actual migration took seconds:

```bash
wp 84em dynamic-years migrate
```

Every instance updated consistently. No missed pages, no typos, no "13 years" on one page and "14 years" on another.

## What AI Handled vs. What I Did

**Claude Code handled:**
- Database analysis and scope assessment
- Solution architecture and trade-off analysis
- Full PHP implementation with WordPress coding standards
- WP-CLI command with dry-run safety
- Case-insensitive pattern matching for variations
- Documentation

**I handled:**
- Describing the problem
- Choosing between proposed solutions
- Reviewing the dry-run output
- Running the final migration
- Verifying a few pages in the browser

The ratio was maybe 10 minutes of my attention for what would have been hours of manual work, and the result was more thorough than I would have achieved alone.

## The Pattern

This workflow applies to any content migration:

1. **Describe the problem** in plain language
2. **Let AI analyze** the scope with database queries
3. **Review proposed solutions** and pick one
4. **Get implementation** with safety features built in
5. **Dry-run first**, then execute

The key insight: AI excels at the tedious parts (finding all instances, writing migration code, handling edge cases) while humans handle the judgment calls (is this the right approach? does the preview look correct?).

---

**Technical details:** The full implementation documentation covers the complete code, testing procedures, and file changes. Available as [Markdown](/files/84em-short-code-swap.md) or [PDF](84em-shortcode-swap.pdf).
