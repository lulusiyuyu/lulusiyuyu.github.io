# PROJECT CONTEXT — lulusiyuyu.github.io 个人博客

> 本文件由 AI Agent 生成，供下一个 Agent 或开发者快速上手本项目。
> 最后更新：2026-02-23

---

## 📌 项目概览

| 项目 | 信息 |
|---|---|
| **项目名称** | 刘时宇个人技术博客 |
| **线上地址** | https://lulusiyuyu.github.io |
| **GitHub 仓库** | https://github.com/lulusiyuyu/lulusiyuyu.github.io |
| **本地路径** | `/home/lsy/rec_sandbox/my-personal-blog` |
| **框架** | Hugo Extended v0.146.0+ |
| **主题** | PaperMod（via Git Submodule） |
| **部署方式** | GitHub Actions → GitHub Pages |
| **分支策略** | 仅 `main` 分支，push 自动触发 CI/CD |

---

## 👤 作者信息

| 字段 | 值 |
|---|---|
| **姓名** | 刘时宇 (Liu Shiyu) |
| **GitHub 用户名** | `lulusiyuyu`（注意：早期用户名为 `shiyugood`，已更名）|
| **邮箱** | shiyuliu.dev@qq.com / 2542310322@qq.com |
| **Git 全局配置** | `user.name=lulusiyuyu` / `user.email=2542310322@qq.com` |
| **身份** | 华南师范大学 软件工程 学术型硕士（研二），推荐系统方向 |
| **求职方向** | 后端开发 / 推荐系统 / 搜索与广告推送（实习）|

---

## 🌐 网络与 SSH 配置

### SSH 密钥（已配置免密登录 GitHub）
- 私钥路径：`~/.ssh/id_ed25519`
- 公钥已添加到 GitHub 账号

### 关键配置：SSH 走 443 端口
由于本机（WSL 环境）的 22 端口被网络环境屏蔽，已配置 `~/.ssh/config` 走 443 端口：

```
Host github.com
    Hostname ssh.github.com
    Port 443
    User git
```

**此配置已生效**：`ssh -T git@github.com` 验证通过，输出：
`Hi lulusiyuyu! You've successfully authenticated...`

### Git 远程操作
```bash
# 推送
cd /home/lsy/rec_sandbox/my-personal-blog
git add .
git commit -m "your message"
git push origin main   # 免密，无需输入任何账号密码

# 克隆（必须用 SSH 链接）
git clone --recurse-submodules git@github.com:lulusiyuyu/lulusiyuyu.github.io.git
```

---

## 📁 当前项目目录结构

```
my-personal-blog/
├── .github/
│   └── workflows/
│       └── hugo.yaml              # CI/CD：push main 自动构建部署到 GitHub Pages
├── .gitmodules                    # Submodule 配置（PaperMod 主题，HTTPS URL）
├── assets/
│   └── css/
│       └── extended/
│           └── custom.css         # 自定义 CSS 扩展（当前为空，可在此添加）
├── content/
│   ├── about.md                   # 关于我页面（含完整简历内容）
│   └── posts/
│       └── hello-world.md         # 第一篇博文
├── docs/
│   └── PROJECT_CONTEXT.md         # 本文件：AI Agent 上下文记忆
├── layouts/
│   ├── _default/
│   │   └── list.html              # 重写主页模板，注入 About 简历页面的内容且配置多段连贯 Apple 式动效
│   └── partials/
│       └── extend_footer.html     # JS 注入，负责 IntersectionObserver Fade-Up 动效
├── themes/
│   └── PaperMod/                  # 主题（Git Submodule，勿直接修改）
├── hugo.yml                       # Hugo 核心配置（注意：不是 hugo.toml）
└── README.md                      # 项目说明文档
```

---

## ⚙️ Hugo 配置要点（hugo.yml）

```yaml
baseURL: 'https://lulusiyuyu.github.io/'
theme: 'PaperMod'

pagination:
  pagerSize: 5   # 注意：v0.128+ 废弃了旧的 `paginate`，必须用此写法

params:
  profileMode:
    enabled: true  # 启用了首页 Profile 展示模式
    imageUrl: 'https://github.com/lulusiyuyu.png'  # GitHub 头像
```

**重要版本要求**：
- Hugo 必须 ≥ `0.146.0`（PaperMod 最新版要求）
- GitHub Actions workflow 中的 `HUGO_VERSION` 已设为 `0.146.0`

---

## 🚀 GitHub Actions CI/CD 流程

文件：`.github/workflows/hugo.yaml`

- **触发条件**：push 到 `main` 分支
- **构建方式**：下载 Hugo Extended deb 包安装，`hugo --gc --minify`
- **发布方式**：GitHub Pages（Source 设置为 `GitHub Actions`，非 Deploy from Branch）

**⚠️ 注意**：需要在 GitHub 仓库的 Settings → Pages → Build and deployment → Source 处选择 **`GitHub Actions`**，否则部署不生效。

---

## 🎨 自定义扩展方式

| 功能 | 操作 |
|---|---|
| 自定义 CSS | 在 `assets/css/extended/` 下创建 `.css` 文件，Hugo 自动合并 |
| 自定义 JS / DOM | 创建 `layouts/partials/extend_footer.html`（注入在 `</body>` 前）|
| 自定义 `<head>` 内容 | 创建 `layouts/partials/extend_head.html` |
| 覆盖主题模板 | 在 `layouts/` 中创建同路径文件（Hugo 优先加载项目级 layout）|
| 静态资源 | 放入 `static/` 目录，访问路径为 `https://lulusiyuyu.github.io/文件名` |

---

## 📝 常用操作命令

```bash
# 进入项目目录
cd /home/lsy/rec_sandbox/my-personal-blog

# 本地预览（含草稿）
~/.local/bin/hugo server --buildDrafts

# 新建博文
~/.local/bin/hugo new content posts/your-post-name.md

# 提交并部署
git add .
git commit -m "your commit message"
git push origin main

# Hugo 可执行文件位置（手动安装，非系统级）
~/.local/bin/hugo
```

---

## 🐛 已解决过的关键 Bug（历史记录）

| 问题 | 原因 | 解决方案 |
|---|---|---|
| SSH 连接失败 (exit 255) | 22 端口被局域网/代理屏蔽 | `~/.ssh/config` 配置走 443 端口 |
| Actions 无法拉取 PaperMod | `.gitmodules` 用了 SSH URL，Actions 无私钥 | 改为 HTTPS URL |
| Hugo Build 失败 | PaperMod 要求 Hugo ≥ 0.146.0 | 升级 Action 中的 HUGO_VERSION 至 0.146.0 |
| `paginate` 配置报错 | v0.128.0 废弃了该字段 | 改为 `pagination.pagerSize` |
| GitHub Pages 404 | Pages Source 未设置为 GitHub Actions | 手动在 Settings → Pages 中修改 |

---

## 🎨 设计风格偏好（重要！给下一个 Agent 的提示）

> 经过用户明确要求（2026-02-23与02-24），现已全面部署 **Apple 苹果风格** 视觉体系：
> - **简约理念**：大量留白，使用极简配色与 SF Pro Display/Apple 字体。
> - **呼吸动效 (Motion)**：内容区域滚动时触发 Fade-Up 与平滑上滑（通过 IntersectionObserver 在 `extend_footer.html` 实现）。修复了在深色模式下的各种可读性问题，移除了滚动回弹 (OverscrollBounce)。支持**正反双向动画播放**，上滑时剥离可见类，再次遇界即播放，极具质感。包含About大外框也具备此出场效果。
> - **单页动效架构 (Single Page Experience)**：`About` 关于我页面的内容不再通过按钮和菜单单独点击进入，而是直接注入到了主页 (`layouts/_default/list.html`)。所有的段落、标题都附带了滚轮滑下时的 Apple 丝滑展现。
> - **微小细节**：运用 Backdrop-filter（毛玻璃顶部导航/Glassmorphism）、小半径圆角（14px~20px）、Pill 形状按钮（圆角 980px）、微小交互浮动缩放等原生质感 UI。
> - **注意事项**：请勿破坏此风格的纯粹感，严禁再使用高饱和度的渐变光晕/Blob（以前被回滚过），后续若需调整或增加组件，必须符合这种内敛、干练的 Apple 品牌质感。

---

## 📋 待办 / Future Work

- [ ] 写更多技术博文（推荐系统、LLM 服务化、竞赛题解等）
- [ ] 配置自定义域名（如有需要）
- [ ] 添加评论系统（如 Giscus，基于 GitHub Discussions）
- [ ] 引入 Google Analytics 或 Umami（隐私友好统计）
- [ ] **首页视觉优化**（需要用户先提供参考网站再设计，切勿擅自动手）
