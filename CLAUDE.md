# Project Spec: Darshnik's Personal Website + Blog

## Overview
A custom personal website with a blog section, inspired by waitbutwhy.com (warm, editorial, personality-driven long-form writing) and debarghyadas.com (clean personal landing page with curated sections). Built with Astro + Tailwind CSS, deployed on Cloudflare Pages.

## Design Philosophy
- The blog is for long-form, visual, personality-driven essays on sport, history, tech, and the future
- Inspired by WBW's approach: deep research + humor + visual explanations + accessible writing
- The reading experience is EVERYTHING — optimize for 10-20 minute immersive reads
- Support heavy visual content: diagrams, charts, embedded interactive components, images with captions
- MDX support is critical for embedding custom visual components inside blog posts
- Start minimal, iterate as voice/niche emerges

## Tech Stack
- **Framework:** Astro v5 (latest stable)
- **Styling:** Tailwind CSS v4
- **Content:** Markdown/MDX for blog posts (Astro Content Collections)
- **Search:** Pagefind (static search, added post-build)
- **Deployment:** Cloudflare Pages (auto-deploy from GitHub, free tier, 300+ edge CDN)
- **Newsletter:** Buttondown (add later, free tier up to 100 subscribers)
- **Comments:** None for v1 (add Giscus later if needed)
- **Analytics:** None for v1 (add Plausible or Umami later)
- **Package Manager:** pnpm

## Site Structure

```
/                   → Landing page (hero + sections)
/blog               → Blog listing (all posts, filterable by tag)
/blog/[slug]        → Individual blog post
/about              → About page (full story)
/rss.xml            → RSS feed
/sitemap.xml        → Auto-generated sitemap
```

## Page Specs

### Landing Page (/)
The landing page is a single scrollable page with distinct sections:

**Hero Section:**
- Your name prominently displayed
- A one-liner tagline (e.g., "I write about sport, history, tech, and the future.")
- Subtle, warm background — no stock photos, no gradients. Think cream/off-white.
- Optional: small profile photo (circular, not too large)
- Social links (LinkedIn, GitHub, X/Twitter) as minimal icons

**Featured Writing Section:**
- Heading: "Writing" or "Selected Essays"
- 3 featured/pinned blog posts displayed as cards
- Each card: title, short excerpt (2 lines), date, estimated read time, tag
- "View all writing →" link to /blog
- Cards should feel editorial — think newspaper column layout, not tech blog grid

**About Snapshot Section:**
- 2-3 sentences about who you are
- "Read more →" link to /about
- Keep it warm and human, not a LinkedIn summary

**Footer:**
- Social links
- "Built with Astro" or similar subtle credit
- RSS feed link
- Copyright

### Blog Listing (/blog)
- Clean list/card layout of all posts, newest first
- Each post shows: title, date, estimated read time, tags, 2-line excerpt
- Filter/sort by tags: Sport, History, Tech, Future, Life, Misc
- Pagination (8-10 posts per page)
- Search bar (Pagefind)

### Blog Post (/blog/[slug])
**THIS IS THE MOST IMPORTANT PAGE. This is where readers spend 95% of their time.**

- Clean, single-column layout optimized for long-form reading
- Max width ~680px for the content column (optimal reading width)
- Typography: large, readable serif or humanist sans-serif for body text
  - Recommended: Charter, Lora, Source Serif Pro, or system serif stack
  - Body text: 18-20px, line-height 1.7-1.8
  - Headings: bold, slightly larger, clear hierarchy
- Generous paragraph spacing
- Images: full-width within content column, with captions
- Code blocks: styled with syntax highlighting (if needed)
- Metadata at top: title, date, estimated read time, tags
- Author byline (small, subtle)
- Share buttons at bottom (X, LinkedIn, Copy link)
- "Next/Previous post" navigation at bottom
- Table of contents (optional, for longer posts — sticky sidebar or top)

**The reading experience should feel like reading a well-typeset magazine article or a Wait But Why post — warm, inviting, no distractions.**

### About Page (/about)
- Long-form, narrative style (not bullet points)
- Your story: who you are, what you do, what you care about
- Can include photos
- Career journey (LinkedIn → privacy infra → what excites you)
- Personal interests: cricket, fitness, travel, food
- The "why" behind the blog
- Contact info or link to reach you

## Design System

### Color Palette (Warm Editorial)
```
Background:       #FAFAF7 (warm off-white / cream)
Surface:          #F5F5F0 (slightly darker cream for cards)
Text Primary:     #1A1A1A (near-black, not pure black)
Text Secondary:   #6B6B6B (muted gray for metadata)
Accent:           #C05621 (warm burnt orange — for links, tags, highlights)
Accent Hover:     #9C4221 (darker orange on hover)
Border:           #E8E8E3 (subtle warm gray)
Code Background:  #F0EDE8 (warm light gray)
```

### Typography
- **Headings:** Inter, system-ui, or a clean sans-serif — bold, tight letter-spacing
- **Body (blog posts):** Charter, Lora, Source Serif Pro, or Georgia — optimized for reading
- **UI/Navigation:** Inter or system sans-serif — clean, small
- **Monospace (code):** JetBrains Mono or Fira Code

### Spacing & Layout
- Content max-width: 680px (blog posts), 1080px (landing page)
- Generous whitespace everywhere
- Section padding: 80-120px vertical
- Card padding: 24-32px
- Mobile-first responsive design

### Interactions
- Subtle hover effects on links (color shift, no underline → underline)
- Smooth scroll between landing page sections
- Dark mode toggle (secondary — light mode is primary, but include a toggle)
- Page transitions (Astro View Transitions)

## Content Model (Astro Content Collections)

### Blog Post Frontmatter
```yaml
---
title: "The Architecture of Cricket Strategy"
description: "How cricket captains think about game theory without knowing it"
pubDate: 2026-03-14
updatedDate: 2026-03-15   # optional
tags: ["sport", "history"]
featured: true              # shows on landing page
draft: false
heroImage: "./images/cricket-strategy.jpg"  # optional
readingTime: 12             # auto-calculated or manual
---
```

### Tags (predefined)
- sport
- history
- tech
- future
- life
- misc

## Project Structure
```
darshnik-site/
├── public/
│   ├── images/
│   │   └── profile.jpg
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── Navigation.astro
│   │   ├── ThemeToggle.astro
│   │   ├── BlogCard.astro
│   │   ├── TagList.astro
│   │   ├── ShareButtons.astro
│   │   ├── TableOfContents.astro
│   │   ├── HeroSection.astro
│   │   ├── FeaturedWriting.astro
│   │   ├── AboutSnapshot.astro
│   │   └── SEO.astro
│   ├── content/
│   │   ├── blog/
│   │   │   ├── first-post.md
│   │   │   └── hello-world.md
│   │   └── config.ts
│   ├── layouts/
│   │   ├── BaseLayout.astro
│   │   ├── BlogPost.astro
│   │   └── Page.astro
│   ├── pages/
│   │   ├── index.astro
│   │   ├── about.astro
│   │   ├── blog/
│   │   │   ├── index.astro
│   │   │   └── [...slug].astro
│   │   ├── tags/
│   │   │   └── [tag].astro
│   │   └── rss.xml.ts
│   ├── styles/
│   │   └── global.css
│   └── utils/
│       ├── readingTime.ts
│       └── formatDate.ts
├── astro.config.mjs
├── tailwind.config.mjs
├── tsconfig.json
├── package.json
└── CLAUDE.md
```

## Sample Blog Posts (Seed Content)
Include 2-3 sample posts to test the layout:

1. **"Hello World — Why I Started Writing"** (life, 3 min read)
   A short intro post explaining the blog's purpose and what to expect.

2. **"The Most Fascinating Pattern in Cricket History"** (sport/history, 8 min read)
   A longer post to test the reading experience with headings, images, and lists.

3. **"What LinkedIn's 100,000 Tables Taught Me About Data"** (tech, 10 min read)
   A technical-but-accessible post to test code blocks and technical content.

## SEO & Meta
- Dynamic Open Graph images (auto-generated per post)
- Twitter card meta tags
- Structured data (JSON-LD for blog posts)
- Canonical URLs
- Sitemap auto-generation
- RSS feed

## Performance Targets
- Lighthouse: 95+ on all categories
- First Contentful Paint: < 1s
- Zero JavaScript shipped by default (Astro's default behavior)
- Images: lazy-loaded, optimized with Astro Image

## Deployment
- GitHub repository (public or private — your choice)
- Cloudflare Pages connected to the repo
- Auto-deploy on push to main branch
- Preview deployments on PRs
- Free subdomain: yourproject.pages.dev (until custom domain purchased)
- Custom domain: Buy from Cloudflare Registrar or Namecheap (~$10-12/year), point DNS to Cloudflare Pages
- Astro adapter: @astrojs/cloudflare (or just static output mode, which works out of the box)

## Future Additions (NOT for v1)
- Newsletter signup (Buttondown — free, clean, respects privacy)
- Comments (Giscus — GitHub Discussions-based, clean UI)
- Analytics (Plausible — privacy-friendly, no cookies)
- Custom illustrations/diagrams component (for WBW-style visual explanations)
- Interactive data visualizations (React islands in MDX posts)
- "Now" page (/now — what you're currently up to)
- Projects section
- Custom domain setup
- Cross-posting to Substack/Medium for discovery (keep Astro site as canonical)

---

## Build Instructions for Claude Code

### Phase 1: Scaffold
1. Initialize Astro project with pnpm
2. Add Tailwind CSS integration
3. Set up the project structure above
4. Configure astro.config.mjs with site URL, integrations
5. Set up Content Collections for blog posts

### Phase 2: Design System
1. Configure Tailwind with the color palette and typography
2. Create BaseLayout with header, footer, theme toggle
3. Import/configure fonts (Inter + Lora or Charter)
4. Create global styles for prose/article content

### Phase 3: Landing Page
1. Build HeroSection component
2. Build FeaturedWriting component (pulls featured posts)
3. Build AboutSnapshot component
4. Assemble index.astro

### Phase 4: Blog
1. Build BlogCard component
2. Build blog listing page with tag filtering
3. Build blog post layout (THE critical page — nail the typography)
4. Add reading time calculation
5. Add share buttons
6. Add next/previous navigation

### Phase 5: About Page
1. Create about.astro with editorial layout
2. Add placeholder content

### Phase 6: Polish
1. Add Pagefind search
2. Add RSS feed
3. Add sitemap
4. Add SEO component with OG tags
5. Add View Transitions
6. Dark mode toggle
7. Mobile responsiveness pass
8. Test Lighthouse scores

### Phase 7: Deploy
1. Initialize git repo
2. Push to GitHub
3. Connect to Cloudflare Pages (login → Create project → Connect GitHub repo → set build command: `pnpm build`, output dir: `dist`)
4. Deploy — site is live at yourproject.pages.dev
5. Test on mobile + desktop
