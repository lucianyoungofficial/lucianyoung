# Hugo 版本不一致导致首页异常

发生日期：2026-07-23。整理日期：2026-09-06。以下日志与结果来自当时的排障记录。

## 现象与环境

Windows 本地使用 Hugo 0.164.0 + PaperMod，`hugo server` 正常；部署到 Vercel 后，首页显示 `<rss version="2.0">`，而非预期 HTML。自定义域名与 Vercel 域名都出现同样问题。

## 关键证据

| 检查 | 当时结果 |
|------|----------|
| 本地构建 | 生成 `public/index.html` 与 `index.xml` |
| 仓库与主题 | 最新代码和 PaperMod submodule 均存在 |
| 域名与 HTTPS | 未发现异常 |
| Vercel 构建日志 | 安装了 Hugo 0.58.2，出现首页布局警告 |

关键日志：

```text
Installing Hugo version 0.58.2
found no layout file for "HTML" for "home"
```

当时云端构建记录为 7 页，本地为 16 页；这是辅助线索，不是固定的页面数量要求。

## 根因与无效尝试

部署环境使用的旧版 Hugo 与项目主题不兼容，未生成预期首页。固定版本后恢复正常。0.58.2 是这次故障日志中的版本，不代表 Vercel 永久使用该默认值。

曾尝试配置：

```toml
[module]
  [module.hugoVersion]
    min = "0.164.0"
```

该配置声明版本兼容性要求，并不负责安装或切换 Vercel 的 Hugo 可执行文件；因此没有改变云端实际使用的版本。这与主题是否通过 Git Submodule 引入不是同一件事。参见 [Hugo 版本配置说明](https://gohugo.io/configuration/module/#hugo-version)。

## 修复与验证

当时在 Vercel 的环境变量中设置 `HUGO_VERSION=0.164.0` 并重新部署，随后首页 HTML 和 PaperMod 恢复正常。

当前仓库将版本固定在 `vercel.json`，自动构建检查也读取此值：

```json
{
  "build": {
    "env": {
      "HUGO_VERSION": "0.164.0"
    }
  }
}
```

修改构建环境后，应检查实际构建日志中的版本、确认 `public/index.html` 已生成，并打开部署后的首页验证。构建进程退出成功不等于页面内容正确。

## 留下的经验

遇到“本地正常、云端异常”，先比较构建日志、工具版本和构建命令，再修改代码。域名、主题和源码检查只保留能支持判断的证据，避免重复排查。
