# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.8] - 2026-01-30

### Changed

- Replaced Inter font with Jost across both sites
- Standardized heading weights (h2, h3 now consistently use font-weight: 600)
- Standardized heading sizes (h2: 1.5rem, h3: 1.25rem on all pages)
- Standardized paragraph and h4-h6 font size to 1.2rem
- Removed inconsistent font-size overrides from .intro, .post-list-compact, and .more-from-84em

## [1.2.7] - 2026-01-28

### Fixed

- Pagination now works on posts listing pages (both sites)
- Home page post list font sizes now match posts page for consistency

## [1.2.6] - 2026-01-20

### Changed

- Updated WordPress plugins post: added Simple History and Wordfence, developer-friendly notes for WP Migrate

## [1.2.5] - 2026-01-20

### Added

- New blog post on 84em.dev: "The WordPress Plugins I Actually Use"

### Changed

- External links now include `nofollow` in addition to `noopener` (both sites)
- Updated AGENTS.md external link documentation to reflect nofollow addition

## [1.2.4] - 2026-01-15

### Added

- New blog post on 84em.ai: "When Claude Code Crashes: Using Claude.ai as a Fallback for Codebase Analysis"
- Web app manifest support for both sites (PWA metadata)

## [1.2.3] - 2026-01-10

### Added

- GitHub Actions status badges to README

## [1.2.2] - 2026-01-10

### Changed

- Moved Privacy link below social icons in footer
- Fixed vertical alignment of separators in footer credits line

## [1.2.1] - 2026-01-10

### Fixed

- Footer text links now have 44px touch targets (WCAG 2.5.8 compliance)

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
