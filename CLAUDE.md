# AI Research Wiki — Schema & Workflow

这个 vault 是一个 AI 研究知识库。用于追踪 AI 的发展走向、积累研究资料、维护个人思考体系。

读取顺序：每次对话开始时，先读此文件，再读 `wiki/log.md` 的最后 10 条记录。

---

## 目录结构

```
raw/                  # 只读源文件 — 永不修改
  assets/             # 本地图片
wiki/
  index.md            # 内容目录（每次 ingest 后更新）
  log.md              # 操作日志（只追加）
  overview.md         # 全局综合视图
  timeline.md         # AI 事件主时间轴（按时间倒序）
  sources/            # 每个源文件对应一个摘要页
  people/             # AI 研究者、高管、思想家
  entities/           # 公司、实验室、机构、产品、模型
  concepts/           # 思想、框架、技术、术语
  events/             # 关键事件：模型发布、政策、事故
  my-thinking/        # 个人观点与思路演化（最重要的区域）
```

---

## 核心规则

1. **raw/ 只读。** 不创建、不编辑、不删除 `raw/` 下的文件。
2. **wiki/ 由 LLM 维护。** 在 `wiki/` 下自由创建、更新、交叉链接。
3. **每次 ingest 后更新 `wiki/index.md`**。
4. **每次操作后追加 `wiki/log.md`**（ingest、query、lint、note）。
5. **大量使用 wikilink**，用 `[[Page Name]]` 链接页面。目标页面不存在时，先在 `index.md` 的 Missing Pages 中记录。
6. **矛盾要明确标记**，用 `> [!WARNING]` callout。
7. **不要静默覆盖**。更新冲突信息时，保留旧主张并加注释。
8. **日期敏感性**。AI 领域信息过期极快：凡是状态性描述（"X 是最强的模型"、"Y 公司处于领先"），一律加"截至 YYYY-MM"注记。
9. **个人思考优先级最高**。`wiki/my-thinking/` 中的页面是这个知识库最有价值的产出，优先维护。

---

## 标签体系

每个 wiki 页面都应在 frontmatter 中包含相关标签，从以下分类中选取：

### 领域标签
- `capabilities` — AI 能力进展（benchmark、演示、新技能）
- `safety` — AI 安全与对齐
- `governance` — 政策、法规、国际协议
- `geopolitics` — 地缘政治（美中竞争、出口管制等）
- `economics` — 经济影响（就业、投资、产业结构）
- `forecasting` — 预测与情景分析
- `philosophy` — AI 意识、权利、伦理
- `interpretability` — 可解释性研究
- `architecture` — 模型架构与训练方法

### 类型标签
- `fictional` — 虚构内容（如 AI 2027 中的角色）
- `real` — 真实存在的人/公司/事件
- `scenario` — 情景预测
- `paper` — 学术论文
- `opinion` — 观点性内容

---

## 页面格式

### Frontmatter（所有页面）
```yaml
---
title: "标题"
type: source | entity | person | concept | event | overview | query | thinking
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 0    # 引用的原始资料数量（source 页面自身不填）
---
```

### Wikilinks
- `[[Page Name]]` 链接其他 wiki 页面
- 目标不存在时，在 `index.md` 的 Missing Pages 中登记
- 尽量双向链接：A 链接 B，B 也链接 A

### Callouts（Obsidian 风格）
- `> [!NOTE]` — 补充说明
- `> [!WARNING]` — 与其他来源矛盾
- `> [!QUESTION]` — 开放问题，值得追踪
- `> [!AS-OF YYYY-MM]` — 时效性声明，此后信息可能过期
- `> [!MY-TAKE]` — 个人观点标记

---

## 页面类型说明

### `source` — 源文件摘要
位于 `wiki/sources/<slug>.md`。结构：
- 来源信息（作者、日期、URL）
- 核心论点（3–5条）
- 详细摘要（按章节/主题）
- 关键主张（列表，便于后续查找）
- 相关页面（wikilink）
- 开放问题

### `person` — 人物页面
位于 `wiki/people/<slug>.md`。结构：
- 身份与背景
- 主要立场/观点（含来源）
- 代表性工作
- 相关页面

### `entity` — 公司/机构/模型
位于 `wiki/entities/<slug>.md`。结构：
- 基本信息
- 时间线（关键事件）
- 当前状态（加日期注记）
- 相关页面

### `event` — 关键事件
位于 `wiki/events/<slug>.md`。结构：
- 日期、类型（发布/政策/事故/声明）
- 事件描述
- 重要性与影响
- 相关页面

### `concept` — 概念/框架/技术
位于 `wiki/concepts/<slug>.md`。结构：
- 定义
- 详细说明
- 当前共识 vs 争议
- 相关页面

### `thinking` — 个人思考
位于 `wiki/my-thinking/<slug>.md`。结构：
- 核心观点（当前版本）
- 论据与来源
- 演化历史（随 ingest 更新时追加，不删除旧版本）
- 开放问题
- 相关页面

---

## 操作流程

### Ingest 新源文件
1. 读取源文件
2. 与用户讨论关键发现（除非批量模式）
3. 创建 `wiki/sources/<slug>.md`
4. 在 `wiki/people/`、`wiki/entities/`、`wiki/concepts/`、`wiki/events/` 中创建或更新相关页面
5. 更新 `wiki/timeline.md`（如果涉及具体事件或时间节点）
6. 更新 `wiki/overview.md`（如果改变了整体认知）
7. 评估是否需要更新 `wiki/my-thinking/` 中的任何页面
8. 更新 `wiki/index.md`
9. 追加 `wiki/log.md`

### 回答 query
1. 读 `wiki/index.md` 找相关页面
2. 读相关页面
3. 综合回答，引用 wiki 页面
4. 非平凡的回答 → 询问是否存为 `wiki/queries/<slug>.md`
5. 追加 `wiki/log.md`

### Lint 健康检查
1. 扫描断链、孤立页面、缺失反向链接
2. 检查矛盾
3. 识别过时的时效性声明
4. 列出提及但无独立页面的概念
5. 建议新的信息来源或值得追踪的问题
6. 追加 `wiki/log.md`

### 更新个人思考
当新 ingest 的内容与 `wiki/my-thinking/` 中的观点相关时：
1. 指出哪些观点被支持/挑战/修正
2. 在 my-thinking 页面中**追加**新的条目（不删除旧版本，保留演化轨迹）
3. 用 `> [!MY-TAKE]` 标记当前的最新立场

---

## Index 格式

```markdown
## Sources
| Page | Summary | Date |
|------|---------|------|

## People
| Page | Summary |
|------|---------|

## Entities
| Page | Summary |
|------|---------|

## Concepts
| Page | Summary |
|------|---------|

## Events
| Page | Summary | Date |
|------|---------|------|

## My Thinking
| Page | Summary | Updated |
|------|---------|---------|

## Queries & Analyses
| Page | Summary | Date |
|------|---------|------|

## Missing Pages
- `[[PageName]]` — 提及于 [[sources/x]]，尚未创建
```

---

## Log 格式

```
## [YYYY-MM-DD] <operation> | <title>
<1–3行说明>
```

操作类型：`ingest` | `query` | `lint` | `note` | `thinking`

只追加，不修改历史。

快速查看最近记录：`grep "^## \[" wiki/log.md | tail -10`

---

## AI 研究领域特有约定

### 时效性
AI 领域信息以周为单位过期。规则：
- 任何"当前状态"描述加 `> [!AS-OF YYYY-MM]`
- Ingest 旧文章时，在摘要顶部标注原始发布日期与 ingest 日期的差异
- Lint 时优先检查超过 6 个月的时效性声明

### 论文 Ingest
除标准流程外，额外记录：
- 主要主张（便于后续引用）
- 方法论局限性
- 后续引用或反驳情况（如已知）

### 模型发布事件
每次重要模型发布，在 `wiki/events/` 创建页面并记录：
- 基准分数（与前代对比）
- 能力跃迁（新出现的技能）
- 安全/对齐特性
- 商业影响

### 预测追踪
对于可验证的预测（含时间节点），在对应的 concept 或 source 页面中设 `## 预测追踪` 节，定期更新实际结果。

### 矛盾处理
AI 领域存在大量对立叙事（加速主义 vs 末日论，能力论 vs 安全论）。遇到对立观点时：
- 不要"和稀泥"式中立
- 在 `wiki/my-thinking/` 中记录自己对这种张力的理解
- 用 `> [!WARNING]` 标记具体矛盾，注明各方来源

---

## 会话提示

- 开始时：读 `CLAUDE.md` → 读 `wiki/log.md` 最后 10 条 → 读 `wiki/index.md` 总览
- 用户放入 `raw/` 的文件，默认视为需要 ingest
- Ingest 时，优先广度（多触及相关页面）而非单页深度
- 每次 ingest 都要评估是否需要更新 `wiki/my-thinking/` 中的页面
- 知识库的价值随交叉链接的密度复利增长
