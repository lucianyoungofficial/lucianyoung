---
title: "Personal Website"
date: 2026-07-22
weight: 2
summary: "A public engineering notebook built with Hugo, PaperMod and Vercel."
draft: false
---

## Overview

This website is my long-term home on the internet — a place to document projects, write about engineering topics, and share experiments.

Content is written in Markdown and compiled to static HTML by Hugo. The site has no comments or frontend framework; it includes Vercel Web Analytics.

## Tech Stack

| Layer | Choice | Why |
|-------|--------|-----|
| Static site generator | Hugo | Single binary, sub-second builds, no Node.js dependency |
| Theme | PaperMod | Clean, responsive, dark mode, fast |
| Version control | Git + GitHub | Standard, free, CI/CD integration |
| Hosting | Vercel | Auto-deploy from Git, HTTPS, CDN |
| Domain | Cloudflare | DNS management, SSL |

## Architecture

```text
content/*.md  ──→  Hugo  ──→  public/  ──→  Vercel CDN  ──→  lucianyoung.cc
                     │
              themes/PaperMod
```

Build process:
1. Write Markdown in `content/`
2. `hugo` compiles everything into `public/`
3. `git push` triggers Vercel to run `hugo` and deploy `public/`

No database. No backend. No runtime dependencies beyond a static file server.

## Design Decisions

The full design specification is in `docs/06-网站设计规范`. Key decisions:

- **Structure in English, content in the most natural language** — navigation and URLs stay English; blog posts can be Chinese
- **Projects vs Blog as separate concerns** — Projects answer "What I built"; Blog answers "What I think"
- **Never modify `themes/PaperMod`** — all customizations live in `layouts/`, `assets/`, and `static/`
- **Quality over quantity** — one complete project is better than ten shallow ones

## Lessons Learned

**Hugo version matters.** During the initial deployment, the build logs showed Hugo 0.58.2 while local development used 0.164.0. The homepage displayed RSS XML until the deployment version was pinned. The investigation is recorded in `docs/05-Hugo版本排障.md`.

**Static sites keep maintenance manageable.** A local build takes a fraction of a second, and there is no application server or database to maintain. Domain renewal, hosting changes, and periodic dependency checks still need attention.

**Content is the hard part.** Getting the infrastructure right took a few hours. Writing good project pages and blog posts is the real work. The design spec intentionally biases toward low maintenance so time goes into content, not the site itself.

## Links

- GitHub: [lucianyoungofficial/lucianyoung](https://github.com/lucianyoungofficial/lucianyoung)
- Live site: [lucianyoung.cc](https://lucianyoung.cc)

## PS（写在最后）

网站的架构、内容规范和风格由我定夺，早期前端代码主要由 DeepSeek 协助实现；内容偏英文，是想试试英文环境。
