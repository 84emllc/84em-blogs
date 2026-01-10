# 84EM Blogs

## CI Status

| Site | Build | Lighthouse | Links | External Links |
|------|-------|------------|-------|----------------|
| 84em.ai | [![Build](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-build.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-build.yml) | [![Lighthouse](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-lighthouse.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-lighthouse.yml) | [![Links](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-links.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-links.yml) | [![External](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-external-links.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-ai-external-links.yml) |
| 84em.dev | [![Build](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-build.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-build.yml) | [![Lighthouse](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-lighthouse.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-lighthouse.yml) | [![Links](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-links.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-links.yml) | [![External](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-external-links.yml/badge.svg)](https://github.com/84emllc/84em-blogs/actions/workflows/84em-dev-external-links.yml) |

Monorepo containing two Hugo-based blog sites for 84EM.

| Site | Domain | Focus |
|------|--------|-------|
| [84em.ai](84em.ai/) | https://84em.ai | AI workflows, discoveries, tool reviews |
| [84em.dev](84em.dev/) | https://84em.dev | Web development insights and patterns |

## Quick Start

```bash
# Development server (run from site directory)
cd 84em.ai
hugo server -D

# Production build
hugo
```

## Repository Structure

```
84em-blogs/
├── 84em.ai/           # AI blog
│   ├── content/       # Posts and pages
│   ├── layouts/       # Hugo templates
│   ├── assets/        # CSS (Hugo Pipes)
│   └── static/        # Static files
├── 84em.dev/          # Dev blog (same structure)
├── AGENTS.md          # Project documentation
├── CLAUDE.md          # Points to AGENTS.md
└── README.md          # This file
```

Both sites share identical theme architecture. Changes to layouts, CSS, or shortcodes should be applied to both sites to maintain consistency.

## Deployment

Both sites are hosted on [Kinsta Static Site Hosting](https://kinsta.com/static-site-hosting/). Each site is configured as a separate Kinsta static site pointing to this monorepo.

### How It Works

1. Both Kinsta sites watch this repository (`84emllc/84em-blogs`)
2. Each site uses Kinsta's **Root directory** setting to build from its subdirectory
3. On push to `main`, both sites rebuild (even if only one changed)

### Kinsta Configuration

#### 84em.ai Site

| Setting | Value |
|---------|-------|
| Repository | `84emllc/84em-blogs` |
| Branch | `main` |
| Root directory | `84em.ai` |
| Build command | `hugo` |
| Publish directory | `public` |
| Node.js version | (default) |

#### 84em.dev Site

| Setting | Value |
|---------|-------|
| Repository | `84emllc/84em-blogs` |
| Branch | `main` |
| Root directory | `84em.dev` |
| Build command | `hugo` |
| Publish directory | `public` |
| Node.js version | (default) |

### Setting Up a New Kinsta Static Site

1. Go to [MyKinsta](https://my.kinsta.com/) > Static Sites > Add Site
2. Connect to GitHub and select `84emllc/84em-blogs`
3. Set **Root directory** to the site folder (`84em.ai` or `84em.dev`)
4. Build command: `hugo`
5. Publish directory: `public`
6. Deploy

### Triggering Deployments

- **Automatic:** Push to `main` triggers both sites to rebuild
- **Manual:** In MyKinsta, go to the site > Deployments > Deploy Now

### Preview Deployments

Kinsta creates preview URLs for branches. The URL pattern is:
- 84em.ai: `https://emai-yxxth-branch-{branch-slug}.kinsta.page`
- 84em.dev: `https://emdev-branch-{branch-slug}.kinsta.page`

## CI Workflows

Each site has GitHub Actions workflows in `.github/workflows/`:

- **Lighthouse CI** - Performance, accessibility, SEO audits
- **Link Check** - Validates internal links

Workflows run on push to `main` (with path filters). For PRs, add the `run-ci` label to trigger.

## Documentation

See [AGENTS.md](AGENTS.md) for detailed project documentation including:
- Content creation guidelines
- Design system
- Git workflow
- Writing style guide reference

## Author

[Andrew Miller](https://84em.com) - WordPress development and consulting.

## License

MIT License. See individual site directories for license files.
