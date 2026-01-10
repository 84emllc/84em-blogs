# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2026-01-10

### Changed

- Footer reorganized into 3 distinct lines: copyright, domain links, and credits
- Credits line (Kinsta, Hugo, Source Code) stacks vertically on mobile

### Removed

- "How it's built" section from about pages on both sites

## [1.1.1] - 2026-01-09

### Removed

- RSS/Sitemap validation workflow (xmllint compatibility issues)
- HTML validation workflow (validator false positives on modern CSS)

## [1.1.0] - 2026-01-09

### Added

- Build verification workflow (ensures Hugo builds with expected outputs)
- External link check workflow (weekly, creates issues for broken links)
- Scheduled Lighthouse workflow (weekly performance monitoring with alerts)

### Changed

- Migrated all GitHub Actions workflows to root `.github/workflows/` directory
- Updated workflow path filters for monorepo structure
- Added `workflow_dispatch` trigger to all workflows for manual runs
- Improved security: use environment variables for potentially unsafe inputs

## [1.0.0] - 2026-01-09

### Added

- Monorepo structure consolidating 84em.ai and 84em.dev
- Shared theme architecture across both sites
- Root-level documentation (README.md, AGENTS.md, CLAUDE.md)
- Kinsta static site deployment configuration
- Render hook for external links (auto open in new tab with ↗ indicator)
- GitHub Actions for Lighthouse CI and link checking

### Sites Included

#### 84em.ai
- Hugo static site for AI workflows and tool reviews
- Posts: Hello World, Plan Mode, Sentry MCP, UptimeRobot Tool Evolution, Devil's Advocate, Client Documentation, Git Release History, Content Migration
- Features: Reading time, social sharing, related posts, RSS

#### 84em.dev
- Hugo static site for web development insights
- Posts: Optimizing Since 1995, Dynamic Years Shortcode
- Features: Reading time, social sharing, related posts, RSS
