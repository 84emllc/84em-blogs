# 84EM.DEV

Web development blog sharing insights, patterns, and practical solutions from the field.

**Live site:** https://84em.dev

## Quick Start

```bash
# Development server
hugo server -D

# Build for production
hugo
```

## Creating Posts

Posts with images use page bundles for automatic responsive image generation:

```
content/posts/my-post/
├── index.md      # Post content
├── image1.jpg    # Images in same folder
└── image2.png
```

Reference images with relative paths:

```markdown
![Alt text](image1.jpg)
```

Hugo automatically generates srcset with multiple sizes, converts to WebP, and adds width/height.

## About

Built with Hugo. Minimal JavaScript, no frameworks. Self-hosted Inter font, single CSS file, WCAG 2.2 AA accessible.

By [Andrew Miller](https://84em.com).

## License

MIT License. See [LICENSE](LICENSE) for details.
