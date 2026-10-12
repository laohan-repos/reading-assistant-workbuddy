# 项目长期记忆 — ReadingAssistant（读书助手）

## 项目定位
把「读书总结」全流程封装为可复用 Skill，并为任意书目产出结构化读书总结 Word 文档。

## 关键约定

- **Skill 位置**：`.workbuddy/skills/读书助手/`（项目级）。
  - `SKILL.md` 主入口；`references/content-template.md` 内容规范。
- **固定七板块**：书籍基本信息 / 作者介绍 / 创作背景 / 故事概括 / 内容总结 / 章节分析 / 阅读思考。
- **命名约定**：Word 文档命名为 `书名_作者_日期.docx`，保存在工作区根目录。
- **文档制作路线**：复用内置 `tencent-docx` 的 `full_pipeline`（S1 创作 → S2 美化 → S3 转换）；S2 用 `general` 体裁 + `modern-minimal` 主题，HTML 须过 `html-review` 门禁。
- **高效模板**：`output/9795c077-.../stage2/formatted-活着.html` 是已过门禁（100 分）的版式模板，做新课目时直接替换正文即可，CSS/结构不动，通常一次过门禁。

## 技术要点（避免重复踩坑）

1. `html-review` DT-03：CSS 中所有 margin/padding 必须用 `var(--spacing-*)`，不可用裸值。
2. `html-review` SI-02：每个 `<table>` 必须含 `<thead>`(带 `<th>`) + `<tbody>`。
3. 转 docx：`cd <plugin_root>/skills/html-to-docx/scripts && "$PY" -m html_to_docx convert <in.html> -o <out.docx> --page-size A4 --orientation portrait --margin-top 2.5 --margin-bottom 2.0 --margin-left 2.5 --margin-right 2.5`（`$PY=/Users/alines/.venv-html-to-docx/bin/python`，先跑 `setup-html-to-docx.sh`）。

## Git / 远端

- **主分支**：`main`（本地 `git init -b main`）。
- **git 身份**：程序员老韩 / hanruigang2@gmail.com（全局）；credential.helper = osxkeychain。
- **远端（双仓库）**：
  - `origin` → Gitee：`https://gitee.com/laohan_repos/reading-assistant-work-buddy.git`
  - `github` → GitHub：`https://github.com/laohan-repos/reading-assistant-workbuddy.git`
  - 两者均已建立 `main` 的 upstream 跟踪；`git push origin main` / `git push github main` 分别推送。
- **注意**：两个仓库名略有差异——Gitee 为 `reading-assistant-work-buddy`（带连字符），GitHub 为 `reading-assistant-workbuddy`。
