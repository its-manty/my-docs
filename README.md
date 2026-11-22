# my-docs｜个人技术文档站

这是 `its-manty` 的 MkDocs Material 静态文档实践项目，使用 GitHub Actions 构建并发布到 GitHub Pages。

- [站点首页](https://its-manty.github.io/my-docs/)（首次部署成功后可访问）
- [文档源码](docs/index.md)
- [个人实验报告](report/README.md)（第七步再完善）
- [GitHub Actions 工作流](.github/workflows/deploy.yml)

## 本地预览

在项目根目录执行：

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m mkdocs build --strict
python -m mkdocs serve
```

打开终端输出的本地地址（通常为 `http://127.0.0.1:8000/`）。

## 网站结构

`docs/` 包含首页、关于、使用指南和 API 参考；`mkdocs.yml` 负责网站导航；`.github/workflows/deploy.yml` 负责自动构建和部署。

> 本仓库中的 API 仅供文档示例，不提供后端服务。
