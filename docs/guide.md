# 使用指南

本页记录从本地文档到 GitHub Pages 的基本操作。以下命令以 **Windows PowerShell** 和仓库 `my-docs` 为例；执行前要确保终端当前位于仓库根目录。

## 1. 检查工具和目录

```powershell
git --version
python --version
python -m pip --version
git status
```

项目根目录应包含 `docs/`、`mkdocs.yml` 和 `requirements.txt`。其中 `docs/` 存放页面内容；`mkdocs.yml` 决定导航与主题。

## 2. 创建并启用虚拟环境

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

激活成功后，PowerShell 命令提示符通常会出现 `(.venv)`。虚拟环境只在本地使用，不要上传到 GitHub。

## 3. 在本地构建和预览

先严格检查文档构建：

```powershell
python -m mkdocs build --strict
```

构建成功后启动本地服务器：

```powershell
python -m mkdocs serve
```

终端通常会显示 `Serving on http://127.0.0.1:8000/`。此时用浏览器访问对应地址，依次打开 [首页](index.md)、[关于](about.md)、[API 参考](api.md)，检查导航、表格、代码块和超链接。

!!! tip "浏览器提示“拒绝连接”怎么办？"
    确认执行了 `python -m mkdocs serve`，并且运行服务器的终端没有关闭；访问地址也要带上终端实际显示的端口，例如 `:8000`。检查完可以按 `Ctrl+C` 停止预览。

## 4. 在仓库开启 GitHub Pages

进入自己的仓库，依次选择：

**Settings → Pages → Build and deployment → Source → GitHub Actions**

这一步只是在 GitHub 上选择发布方式；真正的构建和发布过程由 `.github/workflows/deploy.yml` 文件负责。

## 5. 提交修改并推送

确认 `.gitignore` 包含 `.venv/`、`site/` 和 `__pycache__/`，然后执行：

```powershell
git status
git add docs mkdocs.yml requirements.txt .gitignore .github/workflows/deploy.yml README.md
git diff --staged
git commit -m "完善文档站点与自动部署配置"
git push origin main
```

如果本次没有改动的文件，Git 可能提示没有需要提交的内容；这并不一定表示操作出错。

## 6. 检查首次自动部署

在仓库的 **Actions** 页面打开 `Deploy MkDocs to GitHub Pages`，检查 `build` 和 `deploy` 两个任务是否成功，再从 **Settings → Pages** 中获取实际网站地址。

预期的项目站点地址是：

`https://its-manty.github.io/my-docs/`

需要逐个检查四个页面是否可访问，以及导航与代码块是否正常显示。

## 7. 验证修改后自动更新

首次部署成功后，修改 `docs/index.md`，例如增加一行自己编写的说明，再执行：

```powershell
git add docs/index.md
git commit -m "验证文档修改后自动更新网站"
git push origin main
```

这一次**不手动运行工作流**，而是在 Actions 页面观察推送是否自动触发新的运行。运行成功后刷新网站，检查新增内容是否出现。

## 常见问题

| 现象 | 优先检查的内容 |
| --- | --- |
| `No module named mkdocs` | 是否激活虚拟环境并安装 `requirements.txt` |
| 本地网址拒绝连接 | 是否已执行 `mkdocs serve`，端口是否正确 |
| Actions 没有自动运行 | 是否推送到了 `main`，且修改了工作流监控的文件 |
| Actions 的 `build` 失败 | 构建日志、Markdown 链接、YAML 缩进和依赖安装 |
| `build` 成功但 `deploy` 失败 | 仓库 Pages 来源及 Pages 发布权限 |
| 页面没有更新 | 核对第二次运行结果、网站地址并刷新缓存 |

如果想了解工具各自负责什么，可以阅读 [关于本项目](about.md)；如果想练习接口说明的格式，请阅读 [API 参考](api.md)。
