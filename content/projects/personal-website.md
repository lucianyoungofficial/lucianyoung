---
title: "Personal Website"
date: 2026-07-22
weight: 2
summary: "An engineering portfolio built with Hugo, PaperMod and Vercel."
draft: false
---

## Overview

This website is my long-term home on the internet — a place to document projects, write about engineering topics, and share experiments.

It is intentionally minimal. No analytics, no comments, no JavaScript frameworks. Content is written in Markdown and compiled to static HTML by Hugo.

## Tech Stack

| Layer | Choice | Why |
|-------|--------|-----|
| Static site generator | Hugo | Single binary, sub-second builds, no Node.js dependency |
| Theme | PaperMod | Clean, responsive, dark mode, fast |
| Version control | Git + GitHub | Standard, free, CI/CD integration |
| Hosting | Vercel | Auto-deploy from Git, free tier, HTTPS, global CDN |
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

**Hugo version matters.** Vercel defaults to Hugo 0.58.2, but PaperMod v8 requires 0.146+. The deployed site silently served RSS XML instead of HTML until the version was pinned. This took a full evening to diagnose and is documented in `docs/05-Hugo版本排障.md`.

**Static sites are the right call.** The site builds in under 100ms, has zero ongoing cost, and will work for decades without maintenance. No framework rot, no dependency hell.

**Content is the hard part.** Getting the infrastructure right took a few hours. Writing good project pages and blog posts is the real work. The design spec intentionally biases toward low maintenance so time goes into content, not the site itself.

## Links

- GitHub: [lucianyoungofficial/lucianyoung](https://github.com/lucianyoungofficial/lucianyoung)
- Live site: [lucianyoung.cc](https://lucianyoung.cc)

## PS（写在最后）

网站的架构设计、内容规范、外观风格由我完成，前端代码落地大部分是 DeepSeek 写的。一天顶我十几天的工作量，不得不感叹科技改变生活。

网站大部分采用英语，因为想试试英文环境。

GitHub: [lucianyoungofficial/lucianyoung](https://github.com/lucianyoungofficial/lucianyoung)
