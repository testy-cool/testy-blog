# Agent Instructions for testy-blog

This document contains detailed information for AI agents working with this codebase.

## Project Structure

```
.
├── apps
│   └── web                  # Main Next.js application
│       ├── app             # Next.js app directory
│       ├── components      # React components
│       ├── content         # MDX blog posts
│       ├── lib             # Utilities and configs
│       └── public          # Static assets
├── packages
│   ├── ui                  # Shared UI components
│   ├── shadverse          # Shadcn components
│   └── fumadocs-blog      # Blog functionality
└── .github/workflows      # CI/CD workflows
```

## Key Files to Customize

### Core Config Files
- `CNAME` - Custom domain
- `apps/web/blog-configuration.tsx` - Blog settings (siteName, defaultAuthorName, xUsername)
- `apps/web/lib/metadata.ts` - Metadata (name, URLs, Twitter handle)
- `apps/web/app/layout.config.tsx` - Layout config (title, description, owner)

### Component Files
- `apps/web/components/hero.tsx` - Hero section (title, tagline, social links)
- `apps/web/components/simple-footer.tsx` - Footer copyright
- `apps/web/app/layout.tsx` - Page metadata template
- `apps/web/app/blog-og/[[...slug]]/route.tsx` - OG image generation
- `apps/web/app/(home)/layout.tsx` - Home layout social links

### Template Config
- `packages/ui/src/ohimg/template.tsx` - OG image template

### Logo Files
Replace in `apps/web/public/assets/`:
- `logo.svg` - Main logo
- `light-logo.svg` - Logo for light mode (favicon)
- `dark-logo.svg` - Logo for dark mode (favicon)

## Writing Blog Posts

Create MDX files in `apps/web/content/blog/[category]/`:

```mdx
---
title: Your Post Title
description: A brief description of your post
date: 2025-01-02
author: Your Name
tags: [tag1, tag2]
image: https://example.com/og-image.jpg
draft: false
series: optional-series-name
seriesPart: 1
---

Your post content here using MDX...
```

### Frontmatter Fields
- `title` (required) - Post title
- `description` (required) - Post description for SEO
- `date` (required) - Publication date
- `author` (required) - Author name
- `tags` (optional) - Array of tags
- `image` (optional) - Custom OG image URL
- `draft` (optional) - Set to true to hide from production
- `series` (optional) - Series slug to group posts
- `seriesPart` (optional) - Order within series

## Categories and Series

Edit in `apps/web/blog-configuration.tsx`:

```tsx
export const getCategoryBySlug = (slug: string) => {
  const categories = {
    "your-category": {
      label: "Your Category",
      icon: YourIcon,
      description: "Category description",
    },
  };
};

export const getSeriesBySlug = (slug: string) => {
  const series = {
    "your-series": {
      label: "Your Series Name",
      icon: LucideBook,
      description: "Series description",
    },
  };
};
```

## Styling
- Global styles: `apps/web/app/styles/globals.css`
- Tailwind config: `apps/web/tailwind.config.ts`

## Deployment

### Cloudflare Pages
1. Push to GitHub
2. Connect repo in Cloudflare Pages
3. Build command: `pnpm build`
4. Output directory: `apps/web/out`
5. Add `.nvmrc` with `20` for Node version
6. Add `wrangler.toml`:
```toml
name = "your-project-name"
pages_build_output_dir = "apps/web/out"
```

### GitHub Pages
GitHub Actions workflows included. Enable Pages in repo settings, set source to "GitHub Actions".

### Vercel/Netlify
Zero-config deployment, just connect the repo.

## Commands

```bash
pnpm install      # Install dependencies
pnpm dev          # Start dev server
pnpm build        # Build all apps
pnpm lint         # Lint code
pnpm format       # Format code
pnpm check-types  # Type check
```

## Tech Stack
- Next.js 15
- Fumadocs MDX & UI
- Tailwind CSS
- shadcn/ui
- Lucide Icons
- Turborepo
- pnpm
