# Lucian Young：公开的工程笔记本

## 项目简介

使用 Hugo + PaperMod + GitHub + Vercel + Cloudflare 搭建个人网站。

**A place to build, document and share.**

网站用于记录工程实践、项目成果与个人思考，优先积累内容并保持低维护。

> **改进批注（2026-09-06）**：明确网站定位，避免将整个网站误解为只有 Blog 的个人博客。

目标：

- 记录学习过程
- 展示工程项目
- 积累技术文档

---

## 技术栈

- Hugo 0.164.0（由 `vercel.json` 固定）
- PaperMod
- Git
- GitHub
- Vercel
- Cloudflare

---

## 当前进度

- [x] Hugo 初始化
- [x] GitHub 仓库
- [x] 自动部署
- [x] 自定义域名
- [x] HTTPS
- [x] Hugo 版本问题修复
- [x] 首页重构：入口、Current Focus、内容方向与 Featured Work
- [x] Blog：Hello World 首篇文章
- [x] Projects：Network Infrastructure Lab、Personal Website
- [x] Labs：Dino Runner
- [x] About：Who Am I / Current Focus / Contact

> **改进批注（2026-09-06）**：以上勾选表示板块已落地，不代表内容建设结束；具体内容以 `content/` 为准。域名与部署条目沿用原记录，本次只核对本地文件，未重新验证线上服务。

## 后续重点

- 补充值得分享的 Blog 思考与完整 Project 记录。
- 有合适的互动作品时再增加 Labs，不以数量为目标。
- About 的 Email 待作者提供后再添加。

## 本地使用与维护边界

```bash
git submodule update --init --recursive
hugo server
# 发布内容构建（不含草稿）
hugo
# 需要检查草稿时
hugo --buildDrafts
```

- 内容写在 `content/`；自定义放在 `layouts/`、`assets/`、`static/`。
- 不修改 `themes/PaperMod/`，不手动编辑或提交生成目录 `public/`。
- 生产部署沿用 GitHub → Vercel 流程；不要将本地 `public/` 提交到仓库。
- Dino Runner 的音效与 Canvas 清晰度增强需要保留，修改前阅读 `CHANGELOG.md`。

> **改进批注（2026-09-06）**：区分草稿检查与发布构建，并明确主题、生成文件及 Dino 的维护边界。

---

## 文档

- [Hugo 版本排障](docs/05-Hugo版本排障.md)
- [网站设计规范](docs/06-网站设计规范)
- [版本日志](CHANGELOG.md)

> **改进批注（2026-09-06）**：文档入口仅列当前仓库中存在的文件，修正旧名称并移除失效引用。

---

## 工程日志

| 日期 | 内容 |
|------|------|
| 2026-07-21 | Hugo 初始化 |
| 2026-07-22 | GitHub + Vercel 自动部署 |
| 2026-07-23 | 修复 Hugo 版本导致的 XML 首页问题 |
