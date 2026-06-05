# onepage — Agent 开发说明

本仓库托管一个名为 `onepage` 的 Agent Skill，用于把路线图、项目清单、架构说明、实施计划、产品简报、研究摘要页面等结构化材料生成领导可读的单页或分章节展示型 HTML 页面。

## 目录职责

```text
.
├── README.md                     # 英文项目说明
├── README.zh-CN.md               # 中文项目说明
├── AGENTS.md                     # 本文件：Agent 开发与协作约束
├── skills/
│   └── onepage/                  # 可安装的 Skill 源（唯一编辑与发布入口）
│       ├── SKILL.md              # Skill 入口：触发描述、核心流程、输出规则
│       ├── references/
│       │   ├── design-system.md      # 核心方法论：设计原理、模式选择、颜色语义、措辞、检查清单（每次生成都读）
│       │   ├── layout-reference.md   # 布局与组件细节：CSS 布局、架构图指南、组件护栏（构建页面时按需读）
│       │   └── advanced-guide.md     # 高级场景：大内容章节化、迭代指南、已知局限（复杂任务按需读）
│       ├── assets/
│       │   └── report-template.html  # 可复用的单页 HTML 模板
│       └── agents/
│           └── openai.yaml       # UI metadata 和默认调用提示
├── .github/
│   └── workflows/                # 发布与校验工作流
└── releases/                     # 各版本发布说明（releases/<tag>.md）
```

## 硬约束

- `skills/onepage/SKILL.md` 必须保留 YAML frontmatter，且只包含规范需要的元数据。
- `name` 必须是 `onepage`，并与目录名一致。
- `description` 是触发入口，必须同时说明能力和适用场景；不要把触发条件只写在正文里。
- 保持渐进加载：`SKILL.md` 只放核心工作流；核心方法论放到 `references/design-system.md`；布局和组件细节放到 `references/layout-reference.md`；高级场景放到 `references/advanced-guide.md`；可复制模板放到 `assets/`。
- 不要在 `skills/onepage/` 内新增 README、CHANGELOG、INSTALLATION 等辅助文档，避免 skill 目录膨胀。
- 可安装的 Skill 源是 `skills/onepage/`。不要编辑或发布根目录的 skill 文件副本。
- 发布归档必须以 `skills/onepage/` 为内容来源，并以 `onepage/` 作为归档的顶层目录。
- 修改 `skills/onepage/agents/openai.yaml` 时，`default_prompt` 必须显式包含 `$onepage`。
- 默认不要引入外部依赖；这个 skill 应保持可离线使用。只有用户明确要求并接受非离线页面时，才允许外部资源。
- `README.md` 是英文主 README，`README.zh-CN.md` 是中文 README。两个 README 的触发口径、安装方式和发布产物说明必须保持一致。
- 面向 Agent 的安装与更新指南是 `INSTALL.md`。不要新增翻译版安装指南，除非维护模型明确改变。

## 任务路由

- Skill 行为、触发条件和核心工作流：`skills/onepage/SKILL.md`。
- Skill UI metadata 和默认提示：`skills/onepage/agents/openai.yaml`。
- 核心方法论、模式选择、颜色语义和措辞：`skills/onepage/references/design-system.md`。
- 布局、组件和架构图细则：`skills/onepage/references/layout-reference.md`。
- 大内容章节化、迭代和边界场景：`skills/onepage/references/advanced-guide.md`。
- 页面模板：`skills/onepage/assets/report-template.html`。
- Agent 安装与更新说明：`INSTALL.md`。
- 英文项目概览：`README.md`。
- 中文项目概览：`README.zh-CN.md`。
- Release archive 生产：`.github/workflows/release.yml`。
- 发布说明：`releases/<tag>.md`。

## 编辑行为

- 把本仓库视为所发布规则的参考实现。除非请求本身需要替换，否则保留既有结构和视觉语言。
- 保持修改范围收敛到本次请求涉及的 skill 行为、模板、文档、发布或校验逻辑。
- 先改 `skills/onepage/SKILL.md` 的高层规则，再把长内容沉淀到 `skills/onepage/references/design-system.md`。
- 修改触发行为时，优先编辑 `skills/onepage/SKILL.md` frontmatter 的 `description`，必要时同步 `skills/onepage/agents/openai.yaml` 的界面提示。
- 修改页面模板时，保持单文件 HTML、内联 CSS、响应式布局和打印友好。
- 修改发布打包行为时，同时更新 `.github/workflows/release.yml` 和描述发布产物的 README / INSTALL / AGENTS 内容。
- 保留这套报告的核心视觉语言：紧凑 hero、指标卡、sticky 导航、白底 section、8px 圆角、HTML/CSS 架构图、平衡的里程碑卡片。
- 颜色必须有稳定语义：蓝色表示已部署/运行时，绿色表示公共支撑，橙色表示推进中或异步流程，紫色表示外部或独立环境，黄色表示存储，红/粉表示风险或治理。
- 领导可读页面优先使用业务名称；内部 ID、环境变量、实现细节只在必要时作为次级信息出现。
- 架构图如果同时包含物理部署和逻辑应用组织，优先拆成两张图或两个层次。
- 安装与更新流程优先写在 `INSTALL.md`；README 只保留项目概览和快速入口，不承载完整安装排障逻辑。

## 校验

完成修改前，根据变更类型运行相关检查。涉及 skill 源的修改至少运行：

```bash
python3 /Users/GHuang/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/GHuang/WorkSpace/AiProjects/skill-sources/onepage-skill/skills/onepage
```

按需运行：

- 修改 `skills/onepage/SKILL.md` frontmatter 后：

  ```bash
  ruby -e 'require "yaml"; text=File.read("skills/onepage/SKILL.md"); YAML.safe_load(text.split("---",3)[1]); puts "skill frontmatter ok"'
  ```

- 修改 `skills/onepage/agents/openai.yaml` 后：

  ```bash
  ruby -e 'require "yaml"; YAML.load_file("skills/onepage/agents/openai.yaml"); puts "openai yaml ok"'
  ```

- 修改 `.github/workflows/release.yml` 后：

  ```bash
  ruby -e 'require "yaml"; YAML.load_file(".github/workflows/release.yml"); puts "workflow yaml ok"'
  ```

- 修改 README、INSTALL 或发布链接后，搜索陈旧引用：

  ```bash
  rg -n "wjhuang88/onepage($|[^-])|/path/to/onepage$|git pull|INSTALL\\.zh-CN" README.md README.zh-CN.md INSTALL.md .github skills
  ```

重点人工检查：

- `skills/onepage/SKILL.md` frontmatter 是否有效。
- `description` 是否清晰覆盖触发场景。
- `skills/onepage/assets/report-template.html` 是否仍是完整 HTML 文件。
- 桌面和移动布局是否不会重叠、遮挡或溢出。
- 色彩语义是否一致。
- 发布归档验证：本地打包后确认归档顶层目录是 `onepage/`，且内容来自 `skills/onepage/`。

## Git 规则

- 使用 Conventional Commits：
  - `docs:` 用于 README、AGENTS、release notes、skill prose 和 reference 文档。
  - `ci:` 用于 GitHub Actions 和发布打包行为。
  - `fix:` 用于修复命令、校验、链接、安装或发布流程。
  - `feat:` 用于新增 skill 能力、模板能力或发布产物。
- 提交主题尽量使用英文祈使句，`type(scope): description` 格式，scope 可用 `onepage`、`release`、`docs`、`workflow`。
- 不要把无关的发布准备、文档修订和 skill 行为修改混在一个提交里，除非用户明确要求作为同一个发布切片。
- 提交前检查 `git status --short` 和 `git diff --cached --stat`。
- tag 使用语义化版本，例如 `v0.2.1`、`v0.3.0`。推送 `v*` tag 会触发 GitHub Release。
- 推送 `v*` tag 前必须先创建并提交 `releases/<tag>.md`。发布工作流在缺少对应文件时会失败。

## 版本发布流程

发布由 GitHub Actions 工作流 `.github/workflows/release.yml` 执行，只在推送 `v*` tag 时触发。Agent 协助发布时按以下顺序执行，不要跳过本地校验、发布说明和归档结构检查。

1. **确认工作区状态**

   ```bash
   git status --short --branch
   ```

   - 只保留本次发布需要的变更。
   - 如果发现无关的用户改动，不要回滚；先隔离本次发布范围。

2. **确定下一个语义化版本**

   ```bash
   git tag --list 'v*' --sort=-v:refname
   ```

   - tag 格式使用 `v<major>.<minor>.<patch>`，例如 `v0.2.1`。
   - 同步更新 `skills/onepage/SKILL.md` frontmatter 中的 `metadata.version`，值不带 `v`，例如 `"0.2.1"`。

3. **准备发布说明**
   - 新增 `releases/<tag>.md`，例如 `releases/v0.2.1.md`。
   - 使用 `releases/README.md` 中的结构：`Summary`、`Notable Changes`、`Upgrade Notes`。
   - 发布工作流会自动追加 commit 列表和安装说明；release note 文件只写本版本的人类可读摘要。

4. **运行发布相关校验**

   ```bash
   python3 /Users/GHuang/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/GHuang/WorkSpace/AiProjects/skill-sources/onepage-skill/skills/onepage
   ruby -e 'require "yaml"; YAML.load_file(".github/workflows/release.yml"); puts "workflow yaml ok"'
   ```

   - 如果修改了 `skills/onepage/agents/openai.yaml`，额外运行：

   ```bash
   ruby -e 'require "yaml"; YAML.load_file("skills/onepage/agents/openai.yaml"); puts "openai yaml ok"'
   ```

5. **本地验证归档结构**
   - 从仓库根目录打包 `skills/onepage/`，并确认归档顶层目录是 `onepage/`。
   - 示例命令：

   ```bash
   TAG=v0.2.1
   cd /Users/GHuang/WorkSpace/AiProjects/skill-sources/onepage-skill/skills
   zip -r "/tmp/onepage-${TAG}.zip" onepage
   tar -czf "/tmp/onepage-${TAG}.tar.gz" onepage
   unzip -l "/tmp/onepage-${TAG}.zip" | head
   tar -tf "/tmp/onepage-${TAG}.tar.gz" | head
   ```

   - 人工确认归档内容来自 `skills/onepage/`，且解压后直接得到 `onepage/SKILL.md`，不是 `skills/onepage/SKILL.md` 或仓库根目录。

6. **提交发布准备文件**
   - 提交范围通常包括：`skills/onepage/SKILL.md` 的版本号、`releases/<tag>.md`、以及本次功能或文档变更。
   - 不要把本地临时归档文件提交进仓库。
   - 提交前运行：

   ```bash
   git status --short
   git diff --cached --stat
   ```

7. **先推送分支，再推送 tag**

   ```bash
   git push origin main
   git tag <tag>
   git push origin <tag>
   ```

   - tag 必须创建在已经推送的发布提交上。
   - tag push 会触发 GitHub Release；不要在未推送分支提交的情况下单独推送 tag。
   - 工作流会生成并上传：
     - `onepage-<tag>.zip`
     - `onepage-<tag>.tar.gz`
     - `onepage-<tag>.tar.zst`

8. **发布后检查**
   - 在 GitHub Release 页面确认 release body 包含 `releases/<tag>.md` 内容、commit 列表和安装说明。
   - 下载任一归档并确认顶层目录仍是 `onepage/`。
   - 如果 workflow 失败，优先检查：`releases/<tag>.md` 是否存在、`SKILL.md` / `openai.yaml` YAML 是否有效、`report-template.html` 是否是完整 HTML。
   - 汇报时说明 release workflow 已触发，并列出预期归档：`.zip`、`.tar.gz`、`.tar.zst`。

## 会话结束检查

- 汇报改动过的文件，以及每个文件的修改目的。
- 汇报运行过的校验命令和结果。
- 说明未运行的相关检查及原因。
- 如果用户要求提交或发布，结束前确认工作区状态，并在需要时说明是否仍有未提交变更。
- 不要声称发布完成；除非已经确认 GitHub Release 工作流成功并能看到发布产物。tag 推送后只能说发布工作流已触发。

## 当前状态

- 可安装的 Skill 已迁移到 `skills/onepage/`，名称变更为 `onepage`；根目录的旧副本不再维护。
- `quick_validate.py` 基础校验已通过 `skills/onepage/`。
- 发布工作流位于 `.github/workflows/`，发布说明按版本放在 `releases/<tag>.md`。
- 当前目录是 Git 仓库；发布仓库归属为 GitHub owner `wjhuang88`。
