# 关于本项目

## 项目背景

本项目是一个个人技术文档站点实践，重点不是编写复杂的网站程序，而是学习如何把 Markdown 文档变为网页，以及如何使用 GitHub Actions 实现持续部署。

**目标**：将“修改文档 → 提交代码 → 自动生成网页 → 发布网站”串成可重复的流程，并能从 Actions 日志判断构建是否成功。

## 使用的技术

| 工具 | 在本项目中的用途 | 对应文件或位置 |
| --- | --- | --- |
| Markdown | 编写页面标题、段落、表格和代码示例 | `docs/*.md` |
| MkDocs | 读取配置并将 Markdown 构建为静态页面 | `mkdocs.yml` |
| Material for MkDocs | 提供导航、搜索与代码高亮等页面样式 | `mkdocs.yml` 的 `theme` |
| Git | 记录本地修改并推送到远程仓库 | 本地 `.git/` |
| GitHub | 保存源码和版本历史 | `its-manty/my-docs` |
| GitHub Actions | 按工作流自动构建和部署网站 | `.github/workflows/deploy.yml` |
| GitHub Pages | 托管并公开访问静态网站 | 仓库的 `Settings → Pages` |

## 源码、构建产物和公开网站的区别

`docs/` 是**源文件**，包含自己编写的 Markdown；`site/` 是 MkDocs 运行构建命令后生成的**网页文件**，包含 HTML、CSS 等浏览器可使用的资源。

```text
my-docs/
├── docs/                 # 手写 Markdown 页面
│   ├── index.md
│   ├── about.md
│   ├── guide.md
│   └── api.md
├── mkdocs.yml            # 网站名称、主题和导航
├── requirements.txt      # Python 依赖
├── .github/workflows/
│   └── deploy.yml        # 自动构建与部署
├── report/images/        # 实践过程中保存的真实截图
└── site/                 # 构建后生成；不提交到 main
```

构建产物由工具生成，因此不需要直接修改 `site/`，也不需要把它提交到 `main`。这个目录已经写入 `.gitignore`；工作流会在 GitHub 的运行环境中重新构建并上传。

## 工作流的两个任务

1. **build（构建）**：检出代码、配置 Python、安装依赖、运行 `mkdocs build --strict` 并上传 `site/`。
2. **deploy（部署）**：在 `build` 成功后，把构建产物发布到 GitHub Pages。

这样做的好处是将“网页生成”和“网页发布”分开，排查问题时更容易确定出错位置。

## 本次学习重点

我主要关注三个容易混淆的问题：本地预览不等于公网发布；把代码推送到 GitHub 不等于已经完成部署；只修改实验报告也不一定会触发网站更新。

下一步可以根据 [使用指南](guide.md) 验证实际操作过程，也可以在 [API 参考](api.md) 查看技术文档的另一种写法。

返回 [首页](index.md)。
