# AGENTS.md

Project documentation for LLM agents working on this repository.

## Project Overview

**Site:** 84EM.AI
**Domain:** https://84em.ai
**Purpose:** Personal AI resource site sharing AI workflows, discoveries, tool reviews, and practical applications
**Author:** Andrew Miller (also runs [84EM](https://84em.com), a WordPress development consultancy)
**Tone:** Direct, practical, no-hype. Written by a developer for developers.

## Tech Stack

- **Static Site Generator:** Hugo (no theme, custom templates)
- **CSS:** Single hand-written file, processed via Hugo Pipes
- **JavaScript:** Minimal
- **Fonts:** Inter (self-hosted), system stack fallback
- **Hosting:** Static files (deploy `public/` directory)

## Commands

```bash
# Development server with live reload
hugo server -D

# Build for production
hugo

# Create new post
hugo new content posts/my-post-slug.md
```

## Directory Structure

```
84em.ai/
├── .github/
│   └── workflows/
│       ├── lighthouse.yml  # Lighthouse CI (performance, a11y, SEO)
│       └── links.yml       # Internal link validation
├── archetypes/
│   └── default.md          # Frontmatter template for new content
├── assets/
│   └── css/
│       └── main.css        # Single stylesheet (Hugo Pipes processed)
├── content/
│   ├── about.md            # About page
│   └── posts/
│       ├── _index.md       # Posts section config
│       ├── hello-world.md  # Simple post (no images)
│       └── my-post/        # Page bundle (with images)
│           ├── index.md    # Post content
│           └── image.jpg   # Co-located images
├── layouts/
│   ├── _default/
│   │   ├── _markup/
│   │   │   └── render-image.html  # Responsive image processing
│   │   ├── baseof.html     # Base template
│   │   ├── list.html       # Section/taxonomy lists
│   │   └── single.html     # Individual pages/posts
│   ├── partials/
│   │   ├── head.html       # <head> content, CSS, favicons
│   │   ├── header.html     # Site header with nav
│   │   ├── footer.html     # Site footer
│   │   ├── meta.html       # OG, Twitter, SEO meta tags
│   │   └── structured-data.html  # JSON-LD schemas
│   ├── index.html          # Homepage template
│   └── 404.html            # Error page
├── static/
│   ├── images/
│   │   └── logo.webp       # Site logo
│   ├── favicon.ico         # 32x32 favicon
│   ├── icon-192.png        # PWA icon
│   ├── icon-512.png        # PWA icon large
│   ├── apple-touch-icon.png # iOS icon
│   ├── og-image.jpg        # Social share image (1200x630)
│   ├── robots.txt          # Search engine + AI crawler directives
│   └── llms.txt            # LLM-specific site description
├── hugo.toml               # Site configuration
├── AGENTS.md               # This file
└── CLAUDE.md               # Pointer to AGENTS.md
```

## Creating New Posts

Posts with images **must** use page bundles for responsive image generation.

### Post with images (page bundle)

1. Create folder: `content/posts/your-post-slug/`
2. Create `index.md` inside with frontmatter:

```yaml
---
title: "Your Post Title"
slug: "your-post-slug"
date: 2025-12-19
description: "Brief description for SEO and previews"
tags: ["tag1", "tag2"]
---
```

3. Place images in the same folder (not in `/static/images/`)
4. Reference images with relative paths:

```markdown
![Alt text](my-image.jpg)
```

The render hook automatically generates:
- Responsive srcset (400w, 800w, 1200w)
- WebP conversion
- width/height attributes
- lazy loading

### Post without images

```bash
hugo new content posts/your-post-slug.md
```

Edit frontmatter and write content in Markdown.

## Design System

### Brand Colors
- **Primary:** `#004C7E` (deep blue)
- **Primary Dark:** `#003a61`
- **Accent Orange:** `#b54600`
- **Accent Green:** `#4f7705`

### Layout
- **Content max-width:** 720px
- **Wide container:** 1280px (header/nav)
- **Header/Footer:** Black background (#000)

### Dark Mode
Automatic via `prefers-color-scheme`. Primary shifts to `#58a6ff` for contrast.

## Features

### Reading Time
Posts display estimated reading time based on 100 words per minute. This rate is intentionally slower than the typical 200-250 wpm to account for technical content that requires more careful reading.

### Analytics
Site uses [Simple Analytics](https://simpleanalytics.com) for privacy-friendly tracking.

**Disable tracking:** Append `?notrack` to any URL to disable analytics for that page view. Useful for testing or personal browsing.

## Accessibility (WCAG 2.2 AA)

- Skip link to main content
- Semantic HTML landmarks
- 3px focus indicators
- 44px minimum touch targets
- `prefers-reduced-motion` support
- Print stylesheet
- Proper heading hierarchy
- ARIA labels where needed

## SEO & AESEO

### Meta Tags
- Title, description, keywords
- Open Graph (title, description, type, url, image)
- Twitter Cards (summary_large_image)
- Canonical URLs
- Article metadata (published, modified, tags)

### Structured Data (JSON-LD)
- `WebSite` schema on homepage
- `Article` schema on posts

### AI Optimization
- `robots.txt` allows all AI crawlers (GPTBot, Claude-Web, PerplexityBot, etc.)
- `llms.txt` provides site context for LLMs
- Clean semantic HTML for easy parsing

### Feeds
- RSS at `/index.xml`
- XML sitemap at `/sitemap.xml`

## Git Repository

- **Remote:** https://github.com/84emllc/84emai
- **Branch:** main
- **Ignored:** `/public/`, `/resources/_gen/`, editor files

## Git Workflow

**NEVER commit directly to main.** Always create a branch first, then open a PR to merge.

Branch naming:
- `feature/` - New functionality
- `fix/` - Bug fixes and corrections
- `release/` - Version releases
- `hotfix/` - Urgent production fixes

## Versioning Policy

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

**What triggers a version bump:**
- New site features (reading time, share buttons, etc.)
- Infrastructure changes (CI workflows, build config)
- Breaking changes to templates or structure

**What does NOT trigger a version bump:**
- New blog posts (content updates)
- Typo fixes in content
- Minor copy edits

New posts are content, not releases. The changelog tracks site functionality, not content additions.

## CI Workflows

CI workflows run automatically on pushes to `main` (with path filters). For pull requests, workflows only run when the `run-ci` label is added.

### Triggering CI on PRs

Add the `run-ci` label to a PR to trigger:
- **Lighthouse CI** - Performance, accessibility, best practices, and SEO audits
- **Link Check** - Validates all internal links are valid

Results are posted as PR comments.

### Why Label-Based Triggering?

Saves CI minutes by not running expensive checks on every PR commit. Add the label when you're ready for a final review or before merging.

## Configuration Reference

Key settings in `hugo.toml`:

```toml
baseURL = 'https://84em.ai/'
title = '84EM.AI'

[params]
  author = "Andrew Miller"
  description = "Practical AI workflows..."

[params.social]
  twitter = "84emcom"
```

## Deployment

1. Run `hugo` to build
2. Deploy contents of `public/` to static hosting
3. Ensure `baseURL` in `hugo.toml` matches production domain
