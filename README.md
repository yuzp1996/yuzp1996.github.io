# WIP-野望

个人博客，基于 [Hugo](https://gohugo.io/) + [PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题构建。

线上地址：https://yuzp1996.github.io

## 环境准备

```bash
# 安装 Hugo（macOS）
brew install hugo

# 克隆仓库（含主题子模块）
git clone --recursive https://github.com/yuzp1996/yuzp1996.github.io.git
cd yuzp1996.github.io

# 如果已克隆但缺少主题
git submodule update --init --recursive
```

## 本地开发

```bash
hugo server -D
```

访问 http://localhost:1313 ，修改文件后自动热更新。

## 新建文章

```bash
hugo new posts/my-post.md
```

会在 `content/posts/` 下创建新文章，编辑 front matter 中的 `draft: false` 后即可发布。

## 项目结构

```
├── .github/workflows/deploy.yml   # GitHub Actions 自动部署
├── archetypes/default.md          # 新文章模板
├── content/
│   ├── about.md                   # 关于页面
│   ├── archives.md                # 归档页面
│   └── posts/                     # 博客文章
├── hugo.toml                      # 站点配置
└── themes/PaperMod/               # 主题（git submodule）
```

## 部署

推送到 `main` 分支后，GitHub Actions 自动构建并部署到 GitHub Pages，无需手动操作。
