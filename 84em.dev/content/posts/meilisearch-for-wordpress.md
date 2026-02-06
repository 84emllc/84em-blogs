---
title: "Meilisearch for WordPress: A Developer's Honest Take"
slug: "meilisearch-for-wordpress"
date: 2026-02-06
description: "Meilisearch as a WordPress search backend compared to ElasticSearch, Algolia, Relevanssi, and SearchWP. What works, what doesn't, and when it makes sense."
tags: ["wordpress", "meilisearch", "search", "api", "performance"]
---

WordPress default search isn't great. It runs a `LIKE` query against `wp_posts`, ignores relevance, and gets slower as your content grows. Every WordPress developer knows this. The question is what to replace it with.

I recently built a directory site with a few thousand listings that needed fast, typo-tolerant search. I went with Meilisearch. Here's what I learned and how it compares to the alternatives.

## What Meilisearch Is

Meilisearch is an open-source search engine written in Rust. You run it as a standalone service, feed it documents via a REST API, and query it the same way. It handles full-text search, typo tolerance, filtering, faceting, and geo-based sorting out of the box.

Think of it as a simpler alternative to ElasticSearch that prioritizes developer experience over configurability.

## The WordPress Integration

There is no official Meilisearch plugin for WordPress. You build the integration yourself. For my project, that meant:

A PHP indexer class that hooks into `transition_post_status` and syncs documents to Meilisearch whenever a listing is published, updated, or deleted:

```php
add_action(
    hook_name: 'transition_post_status',
    callback: 'LVS\Listings\Search\Indexer::handle_status_change',
    priority: 10,
    accepted_args: 3
);
```

A WP-CLI command for bulk operations:

```bash
# Reindex everything
wp lvs-search index-all

# Index one listing
wp lvs-search index 452
```

And a JavaScript search page that queries Meilisearch directly from the browser:

```javascript
const response = await fetch(`${MEILISEARCH_HOST}/indexes/listings/search`, {
    method: 'POST',
    headers: {
        'Authorization': `Bearer ${SEARCH_KEY}`,
        'Content-Type': 'application/json',
    },
    body: JSON.stringify({ q: query, limit: 50 }),
});
```

The browser talks to Meilisearch directly using a read-only API key scoped to search operations. WordPress is not involved in the query at all.

## What I Like About It

**Setup is fast.** Download a binary, start the service, create an index, push some documents. I had search working in under an hour. Compare that to ElasticSearch, where you're configuring JVM heap sizes before you index your first document.

**Typo tolerance works immediately.** No analyzers to configure, no custom tokenizers to set up. A user searching "vintge" finds "vintage" results without any configuration. Meilisearch handles this by default.

**The API is simple.** One endpoint to add documents. One endpoint to search. One endpoint to update settings. The REST API is well-documented, predictable, and doesn't require learning a query DSL. If you can write a `wp_remote_post` call, you can integrate Meilisearch.

**Resource usage is low.** My instance runs on a small VPS alongside Nginx. It uses about 60MB of RAM for a few thousand documents. ElasticSearch would want at least 1-2GB of heap space for the JVM alone.

**It's self-hosted.** No per-search pricing. No metered API calls. One server, flat cost. For projects with unpredictable search volume, this matters.

**Client-side querying.** Meilisearch supports tenant API keys with read-only, index-scoped permissions. This means the browser can query the search engine directly without routing through WordPress. One fewer round trip, one fewer server to scale.

## What I Don't Like About It

**No WordPress plugin ecosystem.** Algolia has an official WordPress plugin. Relevanssi installs from the WordPress plugin directory. Meilisearch requires custom code for every WordPress integration. You're writing the indexer, the hooks, the CLI commands, and the frontend from scratch. If you're comfortable with that, fine. If you need something a client's team can maintain without a developer, this isn't it.

**Hosting is your problem.** Self-hosting means you manage the server, updates, backups, and uptime. Meilisearch Cloud exists as a hosted option, but then you're paying for infrastructure and you've lost the cost advantage over Algolia.

**No built-in WordPress awareness.** It doesn't know what a custom post type is. It doesn't understand taxonomies or post meta. You flatten all of that into JSON documents yourself. Every new field you want searchable means updating your indexer code and reindexing.

**Limited analytics.** Meilisearch doesn't track what people search for, what they click, or what returns zero results. Algolia gives you a dashboard for all of that. With Meilisearch, you'd build it yourself or go without.

**Smaller community.** When something breaks at 2am, the number of online answers and blog posts about Meilisearch is a fraction of what exists for ElasticSearch or Algolia. The documentation is good, but you're more on your own.

## How It Compares

### vs. WordPress Default Search

This isn't a fair fight. Default WordPress search runs `SELECT * FROM wp_posts WHERE post_content LIKE '%term%'`. No relevance ranking. No typo tolerance. No speed. If your site has more than a few hundred posts, default search is a poor experience for users.

Meilisearch is faster, smarter, and more configurable in every way. The tradeoff is that default search requires zero setup and zero infrastructure.

### vs. Relevanssi

Relevanssi replaces WordPress search with a custom indexing table inside your existing database. It adds relevance ranking, partial matching, and search logging. The free version covers most needs. Premium adds more sorting options and indexing control.

Relevanssi is the practical choice for most WordPress sites. It installs in minutes, works with existing themes, and your client's team can manage it from the admin. No external services. No additional servers.

Choose Meilisearch over Relevanssi when: you need sub-50ms response times, typo tolerance, faceted search, or you're querying from a decoupled frontend. Choose Relevanssi when: your site is a standard WordPress install and you want better search without adding infrastructure.

### vs. SearchWP

SearchWP is a premium WordPress plugin that indexes custom fields, taxonomies, PDF content, and WooCommerce products. It stores its index in the WordPress database and integrates with the native WordPress search template.

Similar to Relevanssi, it's a drop-in improvement that doesn't require external services. It's stronger than Relevanssi for complex content models with lots of custom fields and document attachments.

Choose Meilisearch when: you need speed and a decoupled architecture. Choose SearchWP when: you need deep WordPress integration and your content includes PDFs, custom tables, or WooCommerce products.

### vs. Algolia

Algolia is the closest comparison. Both are dedicated search engines with REST APIs, typo tolerance, and client-side query support.

Algolia's advantages: official WordPress plugin, search analytics dashboard, managed hosting, larger community, and more mature features like AI-powered re-ranking and A/B testing.

Meilisearch's advantages: open source, self-hostable, no per-request pricing, simpler API, and no vendor lock-in.

For a client project where the budget allows it and the team wants managed infrastructure, Algolia is a good choice. For projects where you want full control, predictable costs, and don't need analytics, Meilisearch is worth considering.

Algolia's free tier (10,000 search requests/month) works for small sites. Beyond that, pricing scales with usage and can get expensive for high-traffic sites. Meilisearch self-hosted is a flat server cost regardless of volume.

### vs. ElasticSearch / OpenSearch

ElasticSearch is the industry standard for search at scale. It handles billions of documents, complex aggregations, and geospatial queries.

It's also heavy. The JVM needs at least a few gigs of RAM. Configuration is extensive. The query DSL is powerful but verbose. Cluster management is a skill set unto itself.

For WordPress specifically, ElasticSearch is overkill unless you're running a large multisite or a content platform with millions of posts. ElasticPress (the WordPress plugin) bridges the gap, but you still need to host or pay for an Elastic cluster.

Meilisearch is the right tool when your dataset fits in memory on a single server and you want search working in an afternoon instead of a week.

## When Meilisearch Makes Sense for WordPress

It fits a specific niche:

- **Decoupled or headless WordPress** where the frontend queries search directly
- **Developer-maintained projects** where the team can write and maintain the integration code
- **Cost-sensitive projects** with high search volume where Algolia's per-request pricing adds up
- **Sites that need typo-tolerant, fast search** but don't need analytics or A/B testing
- **Directory or listing sites** where search is a core feature, not an afterthought

It doesn't fit when:

- The client's team needs to manage search without a developer
- You need search analytics and conversion tracking
- Your content model changes frequently and reindexing is a hassle
- You want a plugin you can install and forget about

## The Setup

If you decide to go with it, the infrastructure is straightforward. Install Meilisearch on a VPS, put Nginx in front of it with SSL, and create two API keys: an admin key for the WordPress indexer and a read-only key for the frontend.

```bash
# Install on Ubuntu/Debian
curl -L https://install.meilisearch.com | sh
sudo mv ./meilisearch /usr/local/bin/

# Run with a master key
meilisearch --master-key="your-master-key" --db-path /var/lib/meilisearch/data
```

Create a systemd service so it starts on boot. Point Nginx at port 7700. Generate scoped API keys through the REST API. The whole thing takes less than an hour if you've set up a reverse proxy before.

The WordPress side is a class that builds JSON documents from your post data and pushes them to the Meilisearch API on publish. Maybe 100-150 lines of PHP depending on your content model.

## Bottom Line

Meilisearch is a good search engine. It's fast, simple, and cheap to run. But it's not a WordPress search plugin. There's no admin screen, no settings page, no one-click install. You're building the integration yourself and maintaining it going forward.

For developers working on headless or decoupled WordPress projects, that tradeoff can make a lot of sense. For standard WordPress sites where the client needs to manage things independently, Relevanssi or SearchWP will save everyone time.

Pick the tool that fits the project, not the one that sounds the most interesting. Sometimes the boring solution is the right one.
