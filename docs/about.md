# 关于项目

这个项目是一套用于练习静态文档持续部署的小型样例。它不需要自建服务器，也不需要编写后端程序；重点是理解 **源码、构建与托管** 各自承担的职责。

## 项目目标

1. 用 Markdown 编写有导航的多页文档。
2. 使用 MkDocs Material 把文档转换成静态网页。
3. 使用 GitHub Actions 自动执行构建。
4. 使用 GitHub Pages 发布站点，并验证修改可自动生效。

## 关键工具及分工

| 工具 | 它负责什么 | 主要接触的文件 |
| --- | --- | --- |
| Markdown | 内容写作、标题、表格、链接和代码示例 | `docs/*.md` |
| MkDocs | 读取配置并生成静态网页 | `mkdocs.yml`、`site/` |
| Material for MkDocs | 为网站提供界面主题与导航 | `mkdocs.yml` |
| Git | 记录变更并推送代码 | 各种项目源码 |
| GitHub Actions | 在云端执行自动化任务 | `.github/workflows/deploy.yml` |
| GitHub Pages | 托管构建好的静态文件并提供网址 | 构建产物（Artifact） |

## 文件结构

```text
my-docs/
├── .github/workflows/deploy.yml    # 自动构建与部署工作流
├── docs/
│   ├── index.md                    # 首页
│   ├── about.md                    # 关于
│   ├── guide.md                    # 使用指南
│   ├── api.md                      # API 文档示例
│   └── assets/stylesheets/extra.css
├── report/
│   ├── README.md                   # 个人实验报告
│   └── images/                     # 本人操作截图
├── mkdocs.yml                      # 站点与导航配置
├── requirements.txt                # Python 依赖
├── .gitignore                      # 排除临时与生成文件
└── README.md                       # 仓库入口
```

## 源码和构建产物有什么区别？

- `docs/` 中的 Markdown 是**源文件**，需要自己维护并放入 Git。
- `site/` 是执行 `python -m mkdocs build` 后得到的**输出文件夹**。网页、样式和资源会在这里生成。
- `.gitignore` 排除了 `site/`，避免把每次重建都能得到的产物重复提交到源码分支。
- GitHub Actions 构建成功后，会把 `site/` 作为 Pages Artifact 上传，由部署任务发布。

## 自动部署如何触发？

在工作流中，`push` 指定了 `main` 分支和一组关注的文件路径。更改 `docs/`、`mkdocs.yml`、`requirements.txt` 或工作流文件并推送，就会触发自动构建；仅修改 `report/README.md` 则不会。

此外，`workflow_dispatch` 允许手动执行，以便测试或排查。它和“修改文档后自动触发”的验收要求是两回事。

## 为什么不需要 gh-pages 分支？

这里使用的是 GitHub 官方 Pages Actions 方案：**上传构建产物 → 通过 `deploy-pages` 发布**。因此源码仍保留在 `main`，不必维护另一个存放 HTML 的分支。

## 设计取舍

这套方案适合技术笔记、课程实验记录或简单说明书。优点是维护成本低、更新过程可追踪；局限是 GitHub Pages 提供的是静态托管，不能仅凭这些文件运行真实的后端 API。

可以接着阅读 [使用指南](guide.md)，了解实际如何验证这条发布链路。
