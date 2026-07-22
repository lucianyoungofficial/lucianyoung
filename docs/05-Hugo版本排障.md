# 05 - Hugo 版本排障

**日期：2026-07-23**

---

# 问题描述

个人博客在本地开发环境能够正常运行，但部署到 Vercel 后，首页无法正常显示。

本地：

```bash
hugo server
```

结果：

- 首页正常
- PaperMod 正常加载
- ProfileMode 正常显示

部署到：

```
https://lucianyoung.cc
```

以及：

```
https://lucianyoung.vercel.app
```

浏览器却显示：

```xml
<rss version="2.0">
```

说明访问到的是 RSS，而不是首页 HTML。

---

# 开发环境

| 项目 | 环境 |
|------|------|
| 操作系统 | Windows |
| Hugo | 0.164.0 |
| Theme | PaperMod |
| 部署平台 | Vercel |
| 域名解析 | Cloudflare |

---

# 排查过程

## 1. 检查 Hugo 配置

确认：

- hugo.toml 配置正常
- baseURL 正确
- theme = "PaperMod"
- ProfileMode 配置正常

结果：

✅ 无异常。

---

## 2. 检查本地构建

执行：

```bash
hugo
```

成功生成：

```
public/
├── index.html
├── index.xml
├── blog/
├── projects/
├── labs/
└── about/
```

说明：

Hugo 可以正常生成首页。

结果：

✅ 本地构建正常。

---

## 3. 检查 GitHub

确认：

- 最新代码已 Push
- GitHub 仓库内容完整
- themes/PaperMod 已提交（Git Submodule）

执行：

```bash
git submodule status
```

结果：

```text
themes/PaperMod
```

说明：

主题没有丢失。

结果：

✅ GitHub 正常。

---

## 4. 检查 DNS

确认：

- Cloudflare DNS
- Vercel Domain
- HTTPS

全部正常。

结果：

✅ DNS 无异常。

---

## 5. 检查 Cloudflare

确认：

- 根域名解析正常
- www CNAME 正常
- SSL 正常

结果：

✅ Cloudflare 无异常。

---

## 6. 查看 Build Logs

这是整个排障过程中最关键的一步。

Build Logs 中发现：

```text
Installing Hugo version 0.58.2
```

随后出现大量警告：

```text
found no layout file for "HTML" for "home"
```

最终：

```
Pages | 7
```

而本地：

```
Pages | 16
```

说明：

云端生成的页面数量明显少于本地。

---

# Root Cause（根因分析）

真正原因不是：

- Hugo 配置错误
- PaperMod 错误
- GitHub 错误
- Cloudflare 错误
- DNS 错误

真正原因是：

> **部署环境与本地开发环境的 Hugo 版本不一致。**

本地：

```
Hugo 0.164.0
```

Vercel：

```
Hugo 0.58.2
```

PaperMod 当前版本已经无法兼容 Hugo 0.58。

因此：

- 首页 HTML 没有生成
- Layout 无法解析
- 最终只剩 RSS（index.xml）

浏览器因此显示 XML 页面。

---

# 尝试过的方法

## 方法一

修改：

```toml
[module]
  [module.hugoVersion]
    min = "0.164.0"
```

结果：

无效。

Build Logs 仍然显示：

```
Installing Hugo version 0.58.2
```

原因：

当前项目使用的是 Git Submodule，而不是 Hugo Modules。

因此该配置没有影响 Vercel 使用的 Hugo 版本。

---

# 最终解决方案

进入：

```
Vercel

Project Settings

Environment Variables
```

新增：

| Name | Value |
|------|------|
| HUGO_VERSION | 0.164.0 |

重新部署。

部署完成后：

- Hugo 使用正确版本
- 首页恢复正常
- HTML 正常生成
- PaperMod 正常加载
- ProfileMode 正常显示

---

# 最终结果

网站恢复正常访问：

```
https://lucianyoung.cc
```

自动部署恢复正常。

Build Logs 中不再出现：

```text
Installing Hugo version 0.58.2
```

---

# Lessons Learned

以后如果出现：

```
本地正常
↓

云端异常
```

优先检查：

```
Build Logs
```

重点关注：

- Hugo / Node 等软件版本
- Build Command
- Warning
- Error
- Pages 数量

不要第一时间修改代码。

先确认：

> **部署环境是否与开发环境一致。**

---

# 本次收获

这次问题最大的收获并不是学会了配置 Hugo。

而是建立了一套工程排障思路：

```
现象

↓

验证本地环境

↓

验证代码仓库

↓

验证部署平台

↓

查看 Build Logs

↓

定位 Root Cause

↓

修复部署环境

↓

验证结果
```

很多工程问题并不是代码错误，而是开发环境与部署环境不一致导致的。

因此，Build Logs 应该成为排查部署问题时首先查看的信息，而不是最后才查看。