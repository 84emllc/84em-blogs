# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.4.6] - 2026-01-08

### Fixed

- Move markdown docs to static folder for proper serving

## [1.4.5] - 2026-01-08

### Added

- Markdown alternative to PDF implementation docs for WCAG accessibility

## [1.4.4] - 2026-01-08

### Changed

- Apply green accent color to footer icons and share buttons

## [1.4.3] - 2026-01-08

### Changed

- Remove site title from logo alt attribute

## [1.4.2] - 2026-01-08

### Changed

- Remove underline from header site name link
- Make code block comments white for readability

## [1.4.1] - 2026-01-08

### Changed

- Update header site name color to #9ff400

## [1.4.0] - 2026-01-08

### Added

- Post: AI-Assisted Content Migration
- Site name text in header next to logo
- Table styling for blog posts
- Monokai syntax highlighting for code blocks

## [1.3.0] - 2026-01-07

### Added

- Post: Backfilling Git Release History

## [1.2.1] - 2026-01-07

### Changed

- Hardcode copyright year range to 2025-2026 in footer.
- Add 84EM.TO link to footer navigation.
- Make share buttons heading visible with styled text.
- Change copy button label from "Copy" to "Copy Link".
- Enable robots.txt generation.

## [1.2.0] - 2025-12-20

### Added

- Reading time display on posts (100 wpm for technical content)
- 48x48 favicon for Google Search results (minimum required size)
- CI workflows documentation in AGENTS.md
- Versioning policy documentation in AGENTS.md
- Features documentation (reading time, analytics) in AGENTS.md
- `?notrack` query parameter to disable Simple Analytics
- GitHub Actions for Lighthouse CI and link checking
- PR comments with Lighthouse scores and link check results

### Changed

- CI workflows only run on PRs when `run-ci` label is added
- CI workflows use path filters to skip irrelevant changes

## [1.1.0] - 2025-12-20

### Added

- H2 and H3 heading hierarchy on homepage for accessibility and SEO
- ItemList structured data for blog posts on homepage
- MIT license

### Changed

- License from all rights reserved to MIT

## [1.0.0] - 2025-12-20

### Added

- Hugo static site with blog functionality
- About page with headshot and contact links
- Privacy policy page
- Social share buttons with copy URL functionality
- Related posts feature for blog posts
- Breadcrumbs with structured data for SEO
- Collapsible table of contents for posts
- Table of contents enabled on all page types
- humans.txt for site attribution and philosophy
- llms.txt for AI assistants
- RSS feed with icon in footer
- Self-hosted Inter font with preload optimization
- Simple Analytics integration
- Responsive images with srcset and page bundles
- Sticky header for navigation
- Dark mode with consistent text and footer styling

### Changed

- Post list layout with descriptions and mobile responsive design
- Logo resized for high-DPI displays
- PageSpeed optimizations including inline CSS and resized images

### Infrastructure

- Hugo Extended enabled for image processing
- Kinsta hosting configuration
- hugo-bin for local development builds
