---
title: "WordPress.com Now Has a Claude Connector"
slug: "wordpress-com-claude-connector"
date: 2026-02-05
description: "WordPress.com shipped an official Claude connector built on MCP and OAuth 2.1. What it does, why the hosted vs. self-hosted distinction matters, and what it signals for the broader WordPress ecosystem."
tags: ["wordpress", "claude", "mcp", "ai-integration"]
---

WordPress.com launched an official Claude connector today. It's the first hosted WordPress platform to ship one, and it's built on the MCP and OAuth 2.1 groundwork they've been laying since late 2025.

If you work with WordPress professionally, a few things are worth paying attention to -- and one distinction matters more than the rest.

## What it actually does

The connector gives Claude read-only access to a WordPress.com site's data. Users can ask Claude questions grounded in their real site content: traffic stats, comment summaries, content audits, that sort of thing. It's accessible through Claude's connectors directory, authorized via OAuth 2.1, and revocable at any time.

Setup is straightforward. Enable MCP on your WordPress.com account, choose which tools to expose, and connect through Claude's settings. WordPress.com has a tools reference in their developer docs if you want to see exactly what's available.

## The important distinction: WordPress.com, not WordPress

This is a WordPress.com feature. It requires a paid WordPress.com plan and runs through their hosted infrastructure. If your clients are on self-hosted WordPress (and if you're reading this, most of them probably are), this connector doesn't apply to their sites.

That's not a criticism -- it makes sense that a hosted platform would ship this first. They control the full stack and can guarantee the OAuth flow, MCP endpoints, and permissions model all work together. Self-hosted WordPress doesn't have that luxury, which is why building similar capabilities there requires custom development.

## What this signals for the broader WordPress ecosystem

MCP is becoming the standard interface between AI tools and content platforms. WordPress.com's progression from MCP access in October to OAuth 2.1 in January to an official connector today shows how quickly this is moving. Other hosts and platforms will follow.

Read-only is the starting point, not the destination. Today it's site analysis and content queries. Write access -- creating posts, updating pages, managing settings through AI -- is the obvious next step. When that arrives, the security and permissions questions get more serious.

The gap between hosted and self-hosted WordPress just got wider in one specific area. WordPress.com users get this out of the box. Self-hosted site owners who want similar AI integration capabilities need someone to build it for them.

## What this means if you're building for clients

If you manage WordPress.com sites for clients, this is worth exploring. The read-only access alone could save time on content audits, traffic analysis, and identifying stale content. Point your clients to it and help them get set up.

If you're working with self-hosted WordPress, the more interesting question is what your clients will start asking for once they see what WordPress.com users can do. AI-powered site analysis, content recommendations, automated reporting -- the expectations are being set right now.

The underlying technology (MCP, OAuth 2.1, structured AI access to site data) isn't exclusive to WordPress.com. It can be implemented on self-hosted WordPress with custom development. The difference is that someone has to build and maintain it.

*Source: [WordPress.com Claude Connector announcement ↗](https://wordpress.com/blog/2026/02/05/claude-connector/)*
