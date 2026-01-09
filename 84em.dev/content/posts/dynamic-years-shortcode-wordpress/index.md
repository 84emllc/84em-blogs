---
title: "Never Update \"Years of Experience\" Again: Dynamic Shortcodes in WordPress"
date: 2026-01-08
description: "How to replace hardcoded year references with shortcodes that calculate automatically, so your content stays current without manual updates."
tags: ["wordpress", "automation", "content-management", "shortcodes"]
---

Every year, I have the same task on 84em.com --- find years of experiences references and update them. e.g., "13 years of WordPress experience", "30 years of experience in the industry", etc. Across 60+ pages it's easy to miss a few.

## The Scope of the Problem

A quick database scan showed just how many places needed updating:

| Content Type | Count |
|--------------|-------|
| Pages | 59 |
| Reusable Blocks | 2 |
| Templates | 2 |
| **Total** | 63 |

I had years hardcoded in multiple variations: "30 years of experience," "nearly 30 years of programming," "over 13 years of WordPress development." Some were in hero blocks used across dozens of pages. Others were buried in individual page content.

## The Solution: Calculate Instead of Hardcode

Instead of storing "30 years," I store "since 1995" and let the current year handle the math.

WordPress shortcodes make this straightforward:

```php
const WORDPRESS_START_YEAR   = 2012;
const PROGRAMMING_START_YEAR = 1995;

function calculate_years_since( int $start_year ): int {
    return (int) \date( 'Y' ) - $start_year;
}

// Generic: [years_since year="2012"] → 14 (in 2026)
\add_shortcode(
    tag: 'years_since',
    callback: function ( array $atts ): string {
        $defaults = [ 'year' => (int) \date( 'Y' ) ];
        $atts     = \shortcode_atts( $defaults, $atts, 'years_since' );
        return (string) calculate_years_since( (int) $atts['year'] );
    }
);

// Alias: [wp_years] → WordPress experience since 2012
\add_shortcode(
    tag: 'wp_years',
    callback: fn(): string => (string) calculate_years_since( WORDPRESS_START_YEAR )
);

// Alias: [dev_years] → Programming experience since 1995
\add_shortcode(
    tag: 'dev_years',
    callback: fn(): string => (string) calculate_years_since( PROGRAMMING_START_YEAR )
);
```

Now content reads `[dev_years] years of programming experience` and renders as "31 years of programming experience" in 2026, "32 years" in 2027, and so on.

The generic `[years_since year="YYYY"]` shortcode handles any base year. The aliases are conveniences for frequently-used values.

## Migrating Existing Content

Finding and replacing 68 occurrences by hand would be tedious and error-prone. A WP-CLI command handles it systematically:

```bash
# Preview changes without modifying anything
wp 84em dynamic-years migrate --dry-run

# Execute the migration
wp 84em dynamic-years migrate
```

The migration command searches posts, pages, reusable blocks, and templates. It replaces "30 years" with "[dev_years] years" and "13 years" with "[wp_years] years" using case-insensitive matching.

## Why WP-CLI Over Manual Editing

I could have opened 62 items in the block editor and made text replacements manually. But WP-CLI offers guarantees that manual editing doesn't:

- **Consistency.** Every instance gets the same treatment.
- **Dry-run mode.** Preview exactly what will change before committing.
- **Auditability.** The CLI output shows exactly which items were modified.
- **Speed.** The entire migration takes seconds, not hours.

## Handling Future Content

This only solved existing content. My site also generates pages dynamically via API prompts, so those needed updating too.

The API prompts now include:

> When mentioning years of experience in the content, output [dev_years] for total programming years and [wp_years] for WordPress years (these are WordPress shortcodes).

New pages now use shortcodes from the start.

## The Broader Pattern

This approach works for any calculated value that changes predictably: years since founding, product age, event countdowns. The implementation takes 30 minutes. The time saved compounds every year you skip the manual content audit.

---

**Want the full implementation?** The complete technical write-up includes the full WP-CLI migration command, testing procedures, and file-by-file changes. Available as [Markdown](/files/84em-short-code-swap.md) or [PDF](84em-shortcode-swap.pdf).

**Built with AI assistance.** I used Claude Code to help plan, implement, and test this feature. [Read more on my AI blog ↗](https://84em.ai/posts/ai-assisted-content-migration-from-discovery-to-deployment/).
