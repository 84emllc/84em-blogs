# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.4] - 2026-01-09

### Changed

- Simplified footer domain links to show only extensions (.COM, .DEV, .AI, .TO)
- Added arrow indicator to external footer links

## [1.0.3] - 2026-01-09

### Fixed

- Contact link icons now use correct green (#9ff400) matching footer icons

## [1.0.2] - 2026-01-09

### Changed

- Contact link icons now use accent green color on about pages
- Applied CSS filter to 84em icon image to match SVG icon color

## [1.0.1] - 2026-01-09

### Changed

- Updated GitHub organization links from 84em to 84emllc
- Updated repository links to point to consolidated 84em-blogs monorepo

## [1.0.0] - 2026-01-09

### Added

- Monorepo structure consolidating 84em.ai and 84em.dev
- Shared theme architecture across both sites
- Root-level documentation (README.md, AGENTS.md, CLAUDE.md)
- Kinsta static site deployment configuration

### Sites Included

#### 84em.ai (v1.4.6)
- Hugo static site for AI workflows and tool reviews
- Posts: Hello World, Plan Mode, Sentry MCP, UptimeRobot Tool Evolution, Devil's Advocate, Client Documentation, Git Release History, Content Migration
- Features: Reading time, social sharing, related posts, RSS

#### 84em.dev (v1.2.7)
- Hugo static site for web development insights
- Posts: Optimizing Since 1995, Dynamic Years Shortcode
- Features: Reading time, social sharing, related posts, RSS

### Infrastructure

- GitHub Actions for Lighthouse CI and link checking
- Kinsta static site hosting with monorepo root directory configuration
