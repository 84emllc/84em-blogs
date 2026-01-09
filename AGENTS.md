# AGENTS.md

Project documentation for AI assistants working on this repository.

## Project Overview

**Repository:** 84em-blogs (monorepo)
**Purpose:** Two Hugo-based blog sites sharing similar architecture
**Author:** Andrew Miller ([84EM](https://84em.com))

### Sites

| Site | Domain | Focus |
|------|--------|-------|
| 84em.ai | https://84em.ai | AI workflows, discoveries, tool reviews, practical applications |
| 84em.dev | https://84em.dev | Web development insights, patterns, and practical solutions |

## Tech Stack

- **Static Site Generator:** Hugo Extended (no themes, custom templates)
- **CSS:** Single hand-written file per site (`assets/css/main.css`), processed via Hugo Pipes
- **JavaScript:** Minimal
- **Fonts:** Inter (self-hosted), system stack fallback
- **Hosting:** Kinsta Static (deploy `public/` directory)
- **CI:** GitHub Actions (Lighthouse, link checking)

## Commands

Run from within each site directory (`84em.ai/` or `84em.dev/`):

```bash
# Development server with drafts
hugo server -D

# Production build
hugo

# Create new post (simple)
hugo new content posts/my-post-slug.md

# Create page bundle (for posts with images)
mkdir -p content/posts/my-post-slug
touch content/posts/my-post-slug/index.md
```

## Directory Structure

```
84em-blogs/
├── 84em.ai/                    # AI-focused blog
│   ├── .github/workflows/      # CI (Lighthouse, link check)
│   ├── archetypes/             # Content templates
│   ├── assets/css/main.css     # Styles
│   ├── content/
│   │   ├── about.md
│   │   ├── legal/              # Privacy policy
│   │   └── posts/              # Blog posts
│   ├── layouts/                # Hugo templates
│   ├── static/                 # Static assets
│   ├── hugo.toml               # Site configuration
│   ├── AGENTS.md               # Site-specific docs
│   └── CHANGELOG.md            # Version history
│
├── 84em.dev/                   # Web development blog
│   ├── (same structure)
│
├── AGENTS.md                   # This file
└── CLAUDE.md                   # Pointer to AGENTS.md
```

## Site Configuration

Both sites use identical Hugo configuration structure. Key settings in `hugo.toml`:

```toml
baseURL = 'https://84em.ai/'  # or 84em.dev
title = '84EM.AI'             # or 84EM.DEV

[params]
  author = "Andrew Miller"
  mainSections = ["posts"]

[params.social]
  twitter = "84emcom"

[permalinks]
  posts = "/posts/:slug/"
```

## Creating Content

### Posts with Images (Page Bundle)

1. Create folder: `content/posts/your-post-slug/`
2. Add `index.md` with frontmatter:

```yaml
---
title: "Your Post Title"
slug: "your-post-slug"
date: 2026-01-09
description: "Brief description for SEO and previews"
tags: ["tag1", "tag2"]
---
```

3. Place images in the same folder
4. Reference with relative paths: `![Alt text](image.jpg)`

The render hook generates responsive srcset, WebP conversion, and lazy loading.

### Posts without Images

Simple markdown file: `content/posts/your-post-slug.md`

## Content Guidelines

### Which Site?

| Topic | Site |
|-------|------|
| AI tools, workflows, LLM usage, automation with AI | 84em.ai |
| Web development, WordPress, PHP, JavaScript, performance, hosting | 84em.dev |
| Overlap (e.g., using AI to build a WordPress feature) | Primary on one, cross-link from other |

### Cross-Linking

When a post spans both domains, publish the primary version on the most relevant site and add a cross-link on the other. Example:

> **Built with AI assistance.** [Read more on my AI blog ↗](https://84em.ai/posts/...)

### External Links

All external links (URLs starting with `http`) must:
1. Include ↗ arrow at the end of the link text: `[Link Text ↗](https://example.com)`
2. Open in new tab (handled automatically by `render-link.html` hook)

The render hook at `layouts/_default/_markup/render-link.html` automatically adds `target="_blank" rel="noopener"` to external links. You only need to add the ↗ arrow to the link text.

**Examples:**
- `[GitHub ↗](https://github.com/84emllc)` - external link
- `[Privacy Policy](/legal/privacy-policy/)` - internal link (no arrow)

## Design System

### Brand Colors

- **Primary:** `#004C7E` (deep blue)
- **Primary Dark:** `#003a61`
- **Accent Green:** `#9ff400` (header site name)
- **Accent Orange:** `#b54600`

### Layout

- Content max-width: 720px
- Header/Footer: Black background (#000)
- Dark mode: Automatic via `prefers-color-scheme`

## Features

- **Reading Time:** 100 wpm (slower for technical content)
- **Analytics:** Simple Analytics (`?notrack` to disable)
- **RSS:** `/index.xml`
- **Sitemap:** `/sitemap.xml`

## Accessibility (WCAG 2.2 AA)

- Skip link to main content
- Semantic HTML landmarks
- 3px focus indicators
- 44px minimum touch targets
- `prefers-reduced-motion` support
- Print stylesheet

## SEO

- Open Graph and Twitter Cards
- JSON-LD structured data (WebSite, Article)
- Canonical URLs
- AI crawler friendly (robots.txt allows GPTBot, Claude-Web, etc.)
- llms.txt for LLM context

## Git Workflow

**NEVER commit directly to main.** Always use branches and PRs.

Branch naming:
- `feature/` - New functionality
- `fix/` - Bug fixes
- `release/` - Version releases

## Versioning

Follows [Semantic Versioning](https://semver.org/). Content updates (new posts) do not trigger version bumps. Version changes track site functionality only.

## CI Workflows

Both sites have identical GitHub Actions:

- **Lighthouse CI** - Performance, accessibility, best practices, SEO
- **Link Check** - Validates internal links

Workflows run on push to `main` (with path filters). For PRs, add `run-ci` label to trigger.

## Site-Specific Documentation

For detailed documentation on each site:

- [84em.ai/AGENTS.md](84em.ai/AGENTS.md)
- [84em.dev/CLAUDE.md](84em.dev/CLAUDE.md)
