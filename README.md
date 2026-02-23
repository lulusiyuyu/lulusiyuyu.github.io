# 刘时宇的个人技术博客 | lulusiyuyu.github.io

[![Deploy Hugo site to Pages](https://github.com/lulusiyuyu/lulusiyuyu.github.io/actions/workflows/hugo.yaml/badge.svg)](https://github.com/lulusiyuyu/lulusiyuyu.github.io/actions/workflows/hugo.yaml)

🌐 **在线地址**：[https://lulusiyuyu.github.io](https://lulusiyuyu.github.io)

---

## 📖 简介

这是我的个人技术博客与简历展示站，使用 **Hugo** 静态站点生成器构建，主题为 **PaperMod**，并通过 **GitHub Actions** 自动部署到 **GitHub Pages**。

博客涵盖以下内容：
- 推荐系统 / 多模态学习相关的技术总结
- 后端开发经验与工程实践
- 算法竞赛代码与思路分享
- 个人简历与项目经历

---

## 🛠️ 技术栈

| 工具 | 用途 |
|---|---|
| [Hugo](https://gohugo.io/) v0.146.0+ | 静态站点生成器 |
| [PaperMod](https://github.com/adityatelange/hugo-PaperMod) | 博客主题 |
| [GitHub Actions](https://docs.github.com/en/actions) | 自动构建 & 部署 CI/CD |
| [GitHub Pages](https://pages.github.com/) | 免费静态网站托管 |

---

## 🗂️ 项目结构

```
lulusiyuyu.github.io/
├── .github/
│   └── workflows/
│       └── hugo.yaml          # GitHub Actions 自动部署配置
├── content/
│   ├── about.md               # 关于我 / 简历页
│   └── posts/                 # 博客文章目录
│       └── hello-world.md     # 第一篇博文
├── themes/
│   └── PaperMod/              # 主题（Git Submodule）
├── assets/
│   └── css/
│       └── extended/          # 自定义 CSS 扩展目录
├── layouts/
│   └── partials/              # 自定义 Hugo 模板片段
├── hugo.yml                   # Hugo 核心配置文件
└── README.md                  # 本文件
```

---

## 🚀 本地运行

### 前置要求

- [Hugo Extended v0.146.0+](https://gohugo.io/installation/)
- Git

### 步骤

```bash
# 1. 克隆仓库（含主题 submodule）
git clone --recurse-submodules git@github.com:lulusiyuyu/lulusiyuyu.github.io.git
cd lulusiyuyu.github.io

# 2. 启动本地开发服务器（含草稿）
hugo server --buildDrafts

# 3. 在浏览器中访问
# http://localhost:1313
```

---

## ✍️ 写新博文

```bash
# 新建一篇博文（文件名建议用 kebab-case 英文）
hugo new content posts/my-new-post.md
```

Hugo 会自动生成带有 `draft: true` 的 frontmatter。写完后，将 `draft` 改为 `false`，然后 `git push` 即可自动触发部署。

---

## 📦 自动部署流程

每次向 `main` 分支推送代码时，GitHub Actions 会自动：

1. 安装 Hugo Extended v0.146.0
2. 拉取主题 Submodule（PaperMod）
3. 执行 `hugo --gc --minify` 构建并压缩
4. 将 `public/` 目录发布到 GitHub Pages

整个流程大约需要 **30~60 秒**，完成后网站自动上线。

---

## 🎨 自定义与扩展

| 操作 | 文件位置 |
|---|---|
| 修改站点配置（标题、菜单等）| `hugo.yml` |
| 添加自定义 CSS | `assets/css/extended/custom.css` |
| 添加自定义 JS | `layouts/partials/extend_footer.html` |
| 修改"关于我"页 | `content/about.md` |

---

## 📬 联系

- **Email**：shiyuliu.dev@qq.com
- **GitHub**：[@lulusiyuyu](https://github.com/lulusiyuyu)

---

> 本博客基于 MIT 协议开源，博客内容（文章部分）版权归作者所有。
