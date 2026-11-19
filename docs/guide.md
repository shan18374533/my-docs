# 使用指南

这页集中记录从本地写作到远程自动发布的操作方法。命令以 Python 3.12 和 `main` 分支为例。

## 1. 准备环境

在项目根目录检查 Git 与 Python：

```bash
git --version
python --version
python -m pip --version
```

如果本地命令是 `python3` 或 `py -3.12`，请按系统环境替换。

## 2. 安装依赖

```bash
python -m venv .venv
```

激活虚拟环境后安装依赖（Windows PowerShell 可用 `.venv\Scripts\Activate.ps1`，Git Bash 可用 `source .venv/Scripts/activate`）：

```bash
python -m pip install -r requirements.txt
```

依赖写在 `requirements.txt` 中，可让本机与云端使用相近的主版本环境。

## 3. 本地构建并预览

```bash
python -m mkdocs build --strict
python -m mkdocs serve
```

在浏览器打开命令行显示的地址，通常为 `http://127.0.0.1:8000/`。

检查四个页面是否都能打开、导航是否准确、表格与代码块是否正常。按 `Ctrl+C` 可停止预览服务。

## 4. 配置 GitHub Pages

进入你自己的公开仓库，打开 `Settings → Pages`，在 **Build and deployment → Source** 中选 **GitHub Actions**。

工作流文件为 `.github/workflows/deploy.yml`，其中：

- `build` 任务负责获取源码、安装依赖、生成并上传 `site/`。
- `deploy` 任务依赖 `build`，使用 Pages 所需权限发布上传的资源。
- `workflow_dispatch` 可以手动触发，但自动更新验收应观察 `push` 触发的运行。

## 5. 第一次提交

检查改动内容，再提交到 `main`：

```bash
git status
git add docs mkdocs.yml requirements.txt .gitignore .github/workflows/deploy.yml README.md
git diff --staged
git commit -m "搭建MkDocs文档并配置Pages自动部署"
git push origin main
```

在 GitHub 仓库的 **Actions** 页面确认 `build` 和 `deploy` 两个任务均为成功状态。成功后，从 **Settings → Pages** 或部署记录打开实际站点地址。

## 6. 验证一次自动更新

在 `docs/index.md` 增加一句清楚可辨的新文字，随后执行：

```bash
git add docs/index.md
git commit -m "验证文档修改后自动更新网站"
git push origin main
```

这一步**不要手动点击 Run workflow**。应核对第二次运行是由 `push` 触发，并刷新公开网站查看新增内容。

## 7. 常见问题与定位思路

| 现象 | 优先检查 | 建议操作 |
| --- | --- | --- |
| `mkdocs` 无法运行 | 是否进入虚拟环境、是否安装依赖 | 使用 `python -m pip install -r requirements.txt` |
| `build --strict` 失败 | MkDocs 日志中的警告、文件路径大小写 | 检查 `mkdocs.yml` 和 `docs/` |
| 没有触发 Actions | 是否推送到 `main`、改动文件是否匹配 `paths` | 检查分支与触发规则 |
| 构建成功但不能访问网站 | Pages 发布来源、`deploy` 状态、网址路径 | 确认 Source 是 GitHub Actions，并查看部署日志 |
| 网站仍显示旧内容 | 是否真正发生第二次部署、浏览器缓存 | 先核对 Actions，再强制刷新 |
| 仅修改实验报告没有自动部署 | 报告文件未列入 `push.paths` | 这是预期结果，不需要调整工作流 |

## 8. 完成前自查

- [ ] 四页导航、表格、代码块和页面链接都已检查
- [ ] 首次 `build` 和 `deploy` 均成功
- [ ] 第二次文档推送自动触发运行并更新了页面
- [ ] 实验报告已保存本人真实操作截图

下一步可进入 [API 参考](api.md) 浏览示例接口文档，或回到 [首页](index.md)。
