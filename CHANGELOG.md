# Changelog

## v1.0.3 — 2026-08-07

### Dino Runner 精修（对齐 Chrome 原版）

**音效系统重构**
- 重构脚步声：从按动画帧触发改为固定 ~280ms 一组左右脚双拍节奏，更贴近 Chrome 原版 audio cues
- 起跳逻辑：拦截引擎原本的 `BUTTON_PRESS` 电子嘟声，替换为白噪声 → bandpass 滤波 → 扫频的轻腾空感音效
- 脚步声生命周期管理：起跳瞬间停止脚步循环；落地后恢复并附加轻微落地提示音
- 死亡/暂停/切页/窗口失焦时强制停止脚步循环，防止声音残留
- 热重载清理机制（`__dinoAudioCueCleanup`）：页面脚本重新加载时先清旧定时器
- 修复重启后 `paused` flag 未重置导致脚步声永久消失的 bug
- 保留原版碰撞声（HIT）和计分声不变

**画质优化**
- 修复分数 DPR（125%/150% Windows 缩放）下 Canvas 后备存储分辨率与 2x 精灵图错配：`Math.floor(DPR)=1` 但 `IS_HIDPI=true` 加载 2x sprite → 精灵被 drawImage 双线性插值缩小 → Arcade CSS transform 再放大 → 双重模糊
  - 修复：当 `IS_HIDPI` 时 Canvas 后备存储比率强制 ≥2，精灵渲染像素级 1:1
  - 同时设置 `context.imageSmoothingEnabled = false` 防止任何残留插值
- CSS 布局补齐：
  - `.offline .interstitial-wrapper` 添加 `position: relative`（runner-container 的定位基准）
  - `.arcade-mode .runner-container` 添加 `top: 0`（覆盖普通模式的 `top: 35px` 偏移）

**历史 Dino 改动（7月）**
- 2026-07-27: 低头时帧率对齐（8fps → 12fps），脚步声视觉听觉同步
- 2026-07-27: 低头跑步时音效不中断
- 2026-07-24: 手机端音效频率上移八度，适配手机扬声器
- 2026-07-24: 手机端音效消除爆音
- 2026-07-24: Game Over 后点击/触摸可重新开始
- 2026-07-24: 支持点击/触摸操作，优化音效
- 2026-07-24: 从 wayou/t-rex-runner 移植 Chrome Dino Runner（Chromium ~2015-2017 引擎）

## v1.0.2 — 2026-08-07

- 重构首页为个人作品集式入口
- 新增 Current Focus、What This Site Is For、Featured Work 区块
- 首页增加 Projects / Blog / GitHub 快速入口
- Featured Work 展示 Network Infrastructure Lab、Personal Website、Dino Runner
- 删除首页顶部的 “Vehicle Engineering / Systems / Build Notes” 文案
- 补充首页响应式样式，优化桌面端与移动端展示

## v1.0.1 — 2026-07-27

- 首页导航加入中英对照（Blog → 个人博客 等）
- Dino Runner 脚步音效优化（低头时步调保持一致）

## v1.0.0 — 2026-07-24

- 首页导航 + 中英对照（Blog · Projects · Labs · About）
- Dino Runner 移植到 Labs（Chromium 原版引擎）
- 首页 GitHub 身份链接
- Blog：Hello World! 首篇文章
- Projects：Network Infrastructure Lab / Personal Website
- About 页面（Who Am I / Current Focus / Contact）
- 字体规范：Source Serif 4（标题）/ Geist（正文）/ JetBrains Mono（代码）
- Vercel Web Analytics
- 自定义 footsteps + 跳跃音效
