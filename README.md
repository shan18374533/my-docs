# 02-github-pages｜MkDocs 文档自动部署实验

本仓库是课程实践项目：通过 Markdown 和 **MkDocs Material** 构建四页技术文档；通过 **GitHub Actions** 自动构建，再由 **GitHub Pages** 公开发布。

> **提交前提醒**：这是已备好的项目源码。它不代表已经在你的 GitHub 账号中完成部署；公开网址、个人操作截图和两次 Actions 成功记录需要你实际完成后核验。

## 项目入口

- **公开网站（部署成功后生效）**：https://shan18374533.github.io/my-docs/
- **个人仓库**：https://github.com/shan18374533/my-docs
- **个人实验报告**：[report/README.md](report/README.md)
- **详细操作清单**：[操作清单.md](操作清单.md)
- **教师 Issue 正文草稿**：[教师Issue模板.md](教师Issue模板.md)

## 文件结构

```text
my-docs/
├── .github/workflows/deploy.yml
├── docs/
│   ├── index.md
│   ├── about.md
│   ├── guide.md
│   ├── api.md
│   └── assets/stylesheets/extra.css
├── report/
│   ├── README.md
│   └── images/README.md
├── mkdocs.yml
├── requirements.txt
├── .gitignore
├── personalize.py
├── check_submission.py
├── 操作清单.md
├── 教师Issue模板.md
└── README.md
```

## 首次使用

1. 在 GitHub 创建名为 `my-docs` 的 **Public** 仓库，默认分支 `main`，勾选添加 README。
2. 在本地克隆仓库，把本压缩包 `my-docs/` 目录中的所有内容（包括 `.github/`）复制进克隆目录。
3. 在克隆目录执行下方命令，将占位账号和姓名拼音替换为你自己的信息：

```bash
python personalize.py 你的GitHub用户名 --name 你的姓名拼音
```

4. 安装依赖，严格构建并预览：

```bash
python -m venv .venv
# 根据操作系统激活 .venv 后继续
python -m pip install -r requirements.txt
python -m mkdocs build --strict
python -m mkdocs serve
```

5. 配置 `Settings → Pages → Source → GitHub Actions`，然后按照 [操作清单](操作清单.md) 推送并核对构建、部署和第二次自动更新。

## 本地自检

```bash
python check_submission.py
```

自检会提醒哪些截图、个人信息或链接尚未完善。它只能检查本地文件，**不能代替** GitHub 上真实的构建日志、网站访问及 Issue 提交。

## 文档内容

| 页面 | 重点 |
| --- | --- |
| [首页](docs/index.md) | 项目目标、自动部署流程、站内导航 |
| [关于项目](docs/about.md) | 技术分工、目录结构、源码与产物 |
| [使用指南](docs/guide.md) | 构建、发布、自动更新及排错 |
| [API 参考](docs/api.md) | 虚构 API 示例、JSON、表格、字段解释 |

本项目按课程给出的官方 Pages Actions 发布方案配置，不使用 `gh-pages` 分支，也不需要填写个人访问令牌。
