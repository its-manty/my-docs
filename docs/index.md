# 我的技术文档

欢迎来到 **its-manty 的 MkDocs 文档站**！这是一个围绕“用 GitHub Actions 自动部署静态文档”搭建的学习项目。

本网站采用 Markdown 编写内容，MkDocs Material 生成页面，并计划通过 GitHub Actions 发布到 GitHub Pages。它不依赖数据库或后端服务器，适合作为课程笔记与技术文档站点。

## 从哪里开始？

| 页面 | 主要内容 | 适合什么时候阅读 |
| --- | --- | --- |
| [关于本项目](about.md) | 实践目标、技术组成和文件结构 | 想弄清楚每个工具的作用时 |
| [使用指南](guide.md) | 本地环境、预览、提交和部署检查 | 想自己操作并复现流程时 |
| [API 参考](api.md) | 使用接口示例练习技术文档写法 | 想学习参数和 JSON 格式时 |

## 本次实践要解决什么问题？

过去，如果修改了一篇文档，可能还需要手动复制网页文件到服务器。本次实践希望形成一个更简单的流程：

1. 在 `docs/` 中修改 Markdown。
2. 使用 Git 提交并推送到 GitHub 的 `main` 分支。
3. 由 GitHub Actions 自动安装依赖、构建网页。
4. GitHub Pages 发布构建产物，读者通过网页地址看到更新后的内容。

```text
Markdown 文档 → GitHub 仓库 → GitHub Actions → MkDocs 构建 → GitHub Pages
```

## 项目基本信息

- **GitHub 用户名**：`its-manty`
- **源码仓库**：[its-manty/my-docs](https://github.com/its-manty/my-docs)
- **网站地址**：[its-manty.github.io/my-docs](https://its-manty.github.io/my-docs/)
- **文档语言**：中文
- **实践主题**：静态文档构建与自动部署

!!! info "说明"
    上方网站地址是项目的预期访问地址；只有 GitHub Actions 部署成功后，才能通过该网址正常访问。

## 本地快速预览

在本地仓库根目录、已激活 Python 虚拟环境后执行：

```powershell
python -m pip install -r requirements.txt
python -m mkdocs build --strict
python -m mkdocs serve
```

浏览器通常打开 `http://127.0.0.1:8000/` 即可预览。更多细节见 [使用指南](guide.md)。

---

想知道这些文件分别有什么作用？继续阅读 [关于本项目](about.md)。
