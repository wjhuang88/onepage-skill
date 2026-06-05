# Onepage

[English →](README.md)

**单页 HTML 报告生成 Skill** — 将结构化材料（路线图、项目清单、架构说明、实施计划、产品简报、研究摘要等）转化为精致的单页或分章节展示型 HTML 报告。

生成物为**自包含的 `.html` 文件**：内联 CSS、无外部依赖、可直接分享、打印或嵌入。面向领导汇报、技术展示、路线图评审等场景。

GitHub 仓库：<https://github.com/wjhuang88/onepage>

---

## 目录结构

```
wjhuang88/onepage/
├── README.md                     # 英文说明
├── README.zh-CN.md               # 中文说明（本文件）
├── skills/
│   └── onepage/
│       ├── SKILL.md              # Skill 入口：核心工作流、内容规则、输出检查清单
│       ├── references/
│       │   └── design-system.md  # 详细设计经验：版式、颜色语义、架构图、大内容章节化、措辞指南
│       ├── assets/
│       │   └── report-template.html  # 可复用的单页 HTML 模板（内联 CSS + 响应式 + 打印友好）
│       └── agents/
│           └── openai.yaml       # UI 元数据和默认调用提示
└── ...                           # 其他仓库级文件（License、CI 等）
```

| 文件 | 用途 |
|---|---|
| `skills/onepage/SKILL.md` | Agent 读取的主入口。包含工作流步骤、内容规则、图表规则、大内容规划策略和输出检查清单。 |
| `skills/onepage/references/design-system.md` | 设计系统的详细参考。Agent 在需要调整布局、颜色、架构图、里程碑卡片、章节化或措辞时读取此文件。 |
| `skills/onepage/assets/report-template.html` | 可直接复制使用的 HTML 模板。包含完整的 CSS 变量、响应式断点、打印样式和占位符结构。 |
| `skills/onepage/agents/openai.yaml` | OpenAI 兼容平台的 UI 配置。定义显示名称、简短描述和默认触发提示。 |

---

## 安装

将 Skill 克隆到本地后，可直接被支持 Skill 协议的 Agent 加载使用：

```bash
git clone https://github.com/wjhuang88/onepage.git
```

加载路径为仓库内的 `skills/onepage/` 目录。

---

## 适用场景

当你需要将以下材料转化为**可分享、可阅读、可打印**的 HTML 页面时使用本 Skill：

- 项目路线图（Roadmap）
- 系统架构说明
- 项目状态清单 / 能力清单
- 实施计划或里程碑追踪
- 产品简报（Product Brief）
- 研究摘要或调查报告
- 技术方案演示
- 运营计划或工作汇报

**典型触发方式**：

> "帮我把这份路线图生成一个展示型 HTML 报告"
>
> "把这个架构说明做成一个可以发给领导看的 HTML 页面"
>
> "生成一个项目状态总结的 HTML 报告，包含架构图和里程碑"

---

## 核心能力

### 1. 自适应页面模式

根据材料类型和受众自动选择最合适的叙事结构：

| 模式 | 适用场景 |
|---|---|
| 执行报告（Executive Report） | 决策简报、项目盘点、状态总览 |
| 技术说明（Technical Explainer） | 概念图、架构、流程、接口、约束、发布计划 |
| 路线图（Roadmap） | 时间线、版本规划、迁移计划 |
| 产品简报（Product Brief） | 定位、受众、场景、功能、差异化、上线计划 |
| 研究摘要（Research Digest） | 发现、证据、主题对比、建议 |
| 项目清单（Project Inventory） | 平台/应用/服务/能力的全局盘点 |
| 运营计划（Operating Plan） | 目标、工作流、依赖、决策、风险控制 |
| 分章节长文（Chaptered Showcase） | 大量材料的主题化组织与展示 |

### 2. 可视化组件

- **紧凑 Hero**：标题 + 副标题 + 元数据标签 + 4-6 个核心指标卡片
- **Sticky 导航**：水平滚动锚点导航，长页面必备
- **指标卡片**：概览、状态、进度等摘要信息
- **HTML/CSS 架构图**：三栏架构网格，支持多层视图
- **里程碑卡片**：带优先级标签（P0/P1）的行动卡片
- **对比矩阵**：多方案、多团队、多系统的并排展示

### 3. 响应式 + 打印友好

- 桌面端：最大宽度 1360px，多栏网格，信息密度高
- 平板端（≤980px）：双栏布局
- 手机端（≤640px）：单栏堆叠
- 打印模式：隐藏导航，去除阴影，分页控制

---

## 设计系统

### 颜色语义

颜色在本 Skill 的报告中承载稳定语义，**同一颜色在整个页面中必须代表同一类事物**：

| 颜色 | 色值 | 语义 |
|---|---|---|
| 🔵 蓝色 | `#1f6feb` | 已部署应用、运行时、主要状态 |
| 🟢 绿色 | `#1b8754` | 公共支撑能力、共享服务、MCP |
| 🟠 橙色 | `#b86600` | 推进中的工作、异步流程、待完成能力 |
| 🟣 紫色 | `#7657c8` | 外部系统、独立部署的服务 |
| 🟡 黄色 | `#8a6d1f` | 存储、持久化 |
| 🔴 红色 | `#c63d32` | 风险、治理、审计、告警 |

### 版式规格

- 正文：`14px / 1.65`，适合中英文混排
- 面板：白色背景 + `8px` 圆角 + 微阴影
- 最大宽度：`1360px`
- 间距系统：卡片间距 `14px`，章节间距 `20px`

---

## 使用方法

### 作为 Agent Skill 使用

本 Skill 遵循标准 Skill 调用协议。Agent 在处理汇报类请求时会自动加载 `skills/onepage/SKILL.md`，按需读取 `skills/onepage/references/design-system.md`，并基于 `skills/onepage/assets/report-template.html` 生成 HTML。

典型调用流程：

```
用户提供原始材料
    ↓
1. Agent 识别受众、场景、材料类型
    ↓
2. 选择页面模式和章节结构
    ↓
3. 基于 report-template.html 生成 HTML
    ↓
4. 参考 design-system.md 调整视觉细节
    ↓
5. 输出自包含的 .html 文件
```

### 直接使用模板

如果你只需要一个干净的 HTML 模板来手动编写报告：

1. 复制 `skills/onepage/assets/report-template.html`
2. 替换所有 `{{PLACEHOLDER}}` 占位符为实际内容
3. 根据需要增减章节、卡片和架构图组件

模板中的主要占位符：

| 占位符 | 内容 |
|---|---|
| `{{REPORT_TITLE}}` | 报告主标题 |
| `{{REPORT_SUBTITLE}}` | 报告副标题 |
| `{{METRIC_*_VALUE}}` / `{{METRIC_*_LABEL}}` | Hero 区域指标 |
| `{{SUMMARY_*_TITLE}}` / `{{SUMMARY_*_TEXT}}` | 概览卡片 |
| `{{APP_*}}` / `{{APP_*_TEXT}}` | 架构图中的应用节点 |
| `{{MILESTONE_*_TITLE}}` / `{{MILESTONE_*_TEXT}}` | 里程碑卡片 |

### 内容编写原则

- **结果先行**：用最清晰的结果、当前状态或待决策事项开头，而非背景叙述
- **业务名称优先**：页面可见标签使用业务名称，内部 ID 和环境变量只在必要时作为次级信息出现
- **单一信息源**：同一能力只在一个位置描述，其他地方通过分类引用
- **一卡一意**：每张卡片只承载一个核心信息，密集证据和表格放到专用区块
- **颜色一致**：同一颜色在页面中始终代表同一语义类别
- **具体措辞**：使用"已完成部署""推进中""待治理"等明确状态词，避免模糊表述

---

## 输出质量检查

生成报告后应检查以下项目：

- [ ] 输出为单一 `.html` 文件，浏览器可直接打开
- [ ] 桌面端布局紧凑可读，移动端自动折叠为单栏
- [ ] 章节标题、卡片、注释对齐整齐
- [ ] 文字无重叠或溢出
- [ ] 架构图列宽一致，颜色语义统一
- [ ] 可正常打印为 PDF
- [ ] 导航锚点可正确跳转
- [ ] 里程碑卡片内容和视觉平衡

---

## 技术约束

- **无外部依赖**：所有 CSS 内联，不依赖 CDN 或外部资源，可离线使用
- **单文件输出**：一个 `.html` 文件包含所有内容
- **浏览器兼容**：使用标准 CSS（Grid、Flexbox、CSS Variables），兼容主流现代浏览器
- **中英文混排**：字体栈优先 PingFang SC / Microsoft YaHei，适合中文展示

---

## 校验

修改 Skill 文件后，运行基础校验（路径指向仓库内的 `skills/onepage/` 目录）：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py /path/to/wjhuang88/onepage/skills/onepage
```

重点人工检查项：

- `SKILL.md` 的 YAML frontmatter 是否有效
- `description` 字段是否清晰覆盖触发场景
- `report-template.html` 是否仍为完整 HTML 文件
- 桌面和移动布局是否正常
- 颜色语义是否一致

---

## License

本 Skill 可自由使用和修改。
