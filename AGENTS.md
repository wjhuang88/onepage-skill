# onepage — Agent 开发说明

本仓库托管一个名为 `onepage` 的 Agent Skill，用于把路线图、项目清单、架构说明、实施计划、产品简报、研究摘要等结构化材料生成领导可读的单页或分章节展示型 HTML 报告。

## 目录职责

```text
.
├── README.md                     # 项目说明（中文）
├── AGENTS.md                     # 本文件：Agent 开发与协作约束
├── skills/
│   └── onepage/                  # 可安装的 Skill 源（唯一编辑与发布入口）
│       ├── SKILL.md              # Skill 入口：触发描述、核心流程、输出规则
│       ├── references/
│       │   └── design-system.md  # 详细版式、颜色语义、架构图和措辞经验
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
- 保持渐进加载：`SKILL.md` 只放核心工作流；详细设计经验放到 `references/`；可复制模板放到 `assets/`。
- 不要在 `skills/onepage/` 内新增 README、CHANGELOG、INSTALLATION 等辅助文档，避免 skill 目录膨胀。
- 可安装的 Skill 源是 `skills/onepage/`。不要编辑或发布根目录的 skill 文件副本。
- 发布归档必须以 `skills/onepage/` 为内容来源，并以 `onepage/` 作为归档的顶层目录。
- 修改 `skills/onepage/agents/openai.yaml` 时，`default_prompt` 必须显式包含 `$onepage`。
- 默认不要引入外部依赖；这个 skill 应保持可离线使用。

## 编辑原则

- 先改 `skills/onepage/SKILL.md` 的高层规则，再把长内容沉淀到 `skills/onepage/references/design-system.md`。
- 修改页面模板时，保持单文件 HTML、内联 CSS、响应式布局和打印友好。
- 保留这套报告的核心视觉语言：紧凑 hero、指标卡、sticky 导航、白底 section、8px 圆角、HTML/CSS 架构图、平衡的里程碑卡片。
- 颜色必须有稳定语义：蓝色表示已部署/运行时，绿色表示公共支撑，橙色表示推进中或异步流程，紫色表示外部或独立环境，黄色表示存储，红/粉表示风险或治理。
- 领导可读页面优先使用业务名称；内部 ID、环境变量、实现细节只在必要时作为次级信息出现。
- 架构图如果同时包含物理部署和逻辑应用组织，优先拆成两张图或两个层次。
- 根目录的 `README.md` 是面向用户的中文项目说明；安装与更新流程在面向 Agent 的安装指南中说明，不要混写在 README 里。

## 校验

修改后至少运行：

```bash
python3 /Users/GHuang/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/GHuang/WorkSpace/AiProjects/skill-sources/onepage-skill
```

重点人工检查：

- `skills/onepage/SKILL.md` frontmatter 是否有效。
- `description` 是否清晰覆盖触发场景。
- `skills/onepage/assets/report-template.html` 是否仍是完整 HTML 文件。
- 桌面和移动布局是否不会重叠、遮挡或溢出。
- 色彩语义是否一致。
- 发布归档验证：本地打包后确认归档顶层目录是 `onepage/`，且内容来自 `skills/onepage/`。

## 当前状态

- 可安装的 Skill 已迁移到 `skills/onepage/`，名称变更为 `onepage`；根目录的旧副本不再维护。
- `quick_validate.py` 基础校验已通过 `skills/onepage/`。
- 发布工作流位于 `.github/workflows/`，发布说明按版本放在 `releases/<tag>.md`。
- 当前目录不是 Git 仓库；如果需要版本化，请先明确仓库归属（GitHub owner `wjhuang88`）再提交。
