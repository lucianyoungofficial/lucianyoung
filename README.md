# Lucian Young

**A place to build, document and share.**

一个公开的工程笔记本，用于记录工程实践、个人思考和互动实验。

[访问网站](https://lucianyoung.cc) · [设计规范](docs/06-网站设计规范) · [变更记录](CHANGELOG.md)

## 当前内容

- Projects：Network Infrastructure Lab、Personal Website。
- Blog：Hello World。
- Labs：Dino Runner。
- About：身份、当前关注方向和 GitHub。

结构保持稳定，后续优先补充有价值的内容。

## 技术栈

Hugo 0.164.0 + PaperMod，使用 GitHub 管理源码、Vercel 部署、Cloudflare 管理域名。无数据库或业务后端；已引入 Vercel Web Analytics。

## 本地使用

安装 Hugo 0.164.0，在仓库根目录初始化主题并预览：

```bash
git submodule update --init --recursive
hugo server
```

默认预览地址为 `http://localhost:1313/`。生产构建运行 `hugo`；检查草稿时运行 `hugo --buildDrafts`。

新增内容使用现有模板，例如：

```bash
hugo new content blog/my-first-note.md
```

新文章默认是草稿，发布前检查内容并设置 `draft: false`。

## 修改与发布

- 文章在 `content/`，首页精选路径在 `hugo.toml` 的 `params.selectedWork`。
- 自定义代码在 `layouts/`、`assets/`、`static/`；不修改 `themes/PaperMod/`。
- 提交源码，不提交生成目录 `public/`。
- GitHub Actions 在 master 推送和面向 master 的 PR 上检查构建，版本读取 `vercel.json`。
- master 推送沿用 Vercel 自动部署；CI 只负责检查，不替代部署，也不自动阻止 Vercel 发布。
- 换行和缩进约定见 `.gitattributes`、`.editorconfig`。

排障参考：[Hugo 版本不一致导致首页异常](docs/05-Hugo版本排障.md)。
