# AI Research Wiki — Schema & Workflow

这个 vault 是一个多领域个人知识库。当前主领域：**AI 研究**。设计上支持未来扩展到其他领域。

读取顺序：每次对话开始时，先读此文件，再读 `wiki/log.md` 的最后 10 条记录。

---

## 目录结构

```
raw/                  # 只读源文件 — 永不修改
  assets/             # 本地图片
wiki/
  index.md            # 主目录（类型视图 + 领域视图）
  log.md              # 操作日志（只追加）
  overview.md         # 全局综合视图
  timeline.md         # AI 事件主时间轴（按时间倒序）
  domains/            # 各领域的汇总入口页
    ai-research.md    # AI 研究领域视图
  papers/             # 学术论文摘要（独立格式）
  sources/            # 非论文来源：文章、报告、情景文档、播客笔记
  people/             # 研究者、高管、思想家
  entities/           # 公司、实验室、机构、产品、模型
  concepts/           # 思想、框架、技术、术语
  events/             # 关键事件：模型发布、政策、事故
  my-thinking/        # 个人观点与思路演化（最重要的区域）
```

---

## Frontmatter（所有页面）

```yaml
---
title: "标题"
type: paper | source | entity | person | concept | event | thinking | query | domain-hub
domain: ai-research | [其他领域]   # 留空表示跨领域
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

### type 说明
| type | 位置 | 用途 |
|------|------|------|
| `paper` | `wiki/papers/` | 学术论文 |
| `source` | `wiki/sources/` | 文章、报告、情景文档、视频笔记等 |
| `entity` | `wiki/entities/` | 公司、实验室、模型、产品 |
| `person` | `wiki/people/` | 研究者、高管、思想家 |
| `concept` | `wiki/concepts/` | 思想、框架、技术、术语 |
| `event` | `wiki/events/` | 模型发布、政策、事故、声明 |
| `thinking` | `wiki/my-thinking/` | 个人观点与演化 |
| `query` | `wiki/queries/` | 存档的分析与问答 |
| `domain-hub` | `wiki/domains/` | 某个领域的汇总入口 |

---

## 页面格式详解

### `paper` — 学术论文

```markdown
---
title: "论文标题"
type: paper
domain: ai-research
tags: []
authors: [Author A, Author B]
venue: NeurIPS 2024
year: 2024
url: https://arxiv.org/...
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# 论文标题

**引用**: Author A, Author B (2024). "论文标题". NeurIPS 2024.
**链接**: [原文](URL)

## 核心主张
- 主张 1（具体、可引用的形式）
- 主张 2

## 方法论
- 用了什么数据/实验设置
- 关键假设

## 关键结果
- 指标 / benchmark 表现（数字化，便于后续比较）

## 局限性
- 方法论局限
- 作者自认的限制

## 与知识库的关联
- 支持 / 挑战了哪些 [[concepts/xxx]]
- 与 [[papers/yyy]] 的关系（支持/矛盾）

## 后续追踪
- 引用情况（随 ingest 更新）
- 已知的反驳或跟进研究
```

### `source` — 非论文来源（文章、报告、情景文档）

```markdown
---
title: "来源标题"
type: source
domain: ai-research
tags: []
author: 作者
published: YYYY-MM-DD
url: https://...
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# 来源标题

**来源信息**：作者，日期，URL

## 核心论点（3–5条）

## 详细摘要（按章节/主题）

## 关键主张（列表）

## 相关页面

## 开放问题
```

### `person` — 人物

```markdown
---
title: "姓名"
type: person
domain:
tags: [real]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

## 身份与背景
## 主要立场/观点（含来源）
## 代表性工作
## 相关页面
```

### `entity` — 公司/机构/模型

```markdown
---
title: "名称"
type: entity
domain:
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

## 基本信息
## 时间线（关键事件，倒序）
## 当前状态（含 [!AS-OF] 标记）
## 相关页面
```

### `event` — 关键事件

```markdown
---
title: "事件名称"
type: event
domain:
tags: []
date: YYYY-MM-DD
event-type: release | policy | incident | announcement | milestone
created: YYYY-MM-DD
---

## 事件描述
## 重要性与影响
## 相关页面
```

### `thinking` — 个人思考

```markdown
---
title: "主题"
type: thinking
domain:
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

## 核心观点（当前版本）
## 论据与来源
## 演化历史（追加，不删除）
## 开放问题
## 相关页面
```

### `domain-hub` — 领域入口页

```markdown
---
title: "领域名称"
type: domain-hub
domain: xxx
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

## 领域概述
## 关键论文
## 关键来源
## 关键人物
## 关键概念
## 关键实体
## 当前开放问题
## 推荐阅读顺序
```

---

## Callouts（Obsidian 风格）

- `> [!NOTE]` — 补充说明
- `> [!WARNING]` — 与其他来源矛盾
- `> [!QUESTION]` — 开放问题，值得追踪
- `> [!AS-OF YYYY-MM]` — 时效性声明
- `> [!MY-TAKE]` — 个人观点标记

---

## 标签体系

### 领域标签
- `capabilities` — AI 能力进展
- `safety` — AI 安全与对齐
- `governance` — 政策、法规
- `geopolitics` — 地缘政治
- `economics` — 经济影响
- `forecasting` — 预测与情景
- `philosophy` — 伦理、意识、权利
- `interpretability` — 可解释性
- `architecture` — 模型架构与训练

### 类型标签
- `fictional` — 虚构内容
- `real` — 真实存在
- `scenario` — 情景预测
- `paper` — 学术论文
- `opinion` — 观点性内容

---

## 核心规则

1. **raw/ 只读。** 不创建、不编辑、不删除 `raw/` 下的文件。
2. **wiki/ 由 LLM 维护。**
3. **每次 ingest 后更新对应领域的 `wiki/domains/<domain>.md`，以及 `wiki/index.md`。**
4. **每次操作后追加 `wiki/log.md`。**
5. **大量使用 wikilink** `[[Page Name]]`。目标不存在时登记 Missing Pages。
6. **矛盾要明确标记**，用 `> [!WARNING]`。
7. **不要静默覆盖**。保留旧主张并加注释。
8. **日期敏感性**。状态性描述加 `> [!AS-OF YYYY-MM]`。
9. **`wiki/my-thinking/` 优先级最高**。每次 ingest 都评估是否需要更新。

---

## 操作流程

### 判断内容类型
拿到 raw/ 下的文件后，先判断：
- 有 DOI / arXiv / 正式学术发表 → **paper**，放入 `wiki/papers/`
- 文章、报告、情景文档、播客笔记 → **source**，放入 `wiki/sources/`
- 判断所属 **domain**（默认 `ai-research`）

### Ingest 论文（paper）
1. 读取源文件
2. 创建 `wiki/papers/<slug>.md`（使用 paper 格式）
3. 更新或创建相关 `wiki/people/`（作者）、`wiki/concepts/`、`wiki/entities/` 页面
4. 更新 `wiki/events/` — 若论文发布本身是重要事件
5. 更新 `wiki/timeline.md`
6. 更新 `wiki/domains/<domain>.md`
7. 评估是否需要更新 `wiki/my-thinking/` 中的页面
8. 更新 `wiki/index.md`
9. 追加 `wiki/log.md`

### Ingest 非论文来源（source）
1. 读取源文件
2. 创建 `wiki/sources/<slug>.md`（使用 source 格式）
3. 更新相关 people / entities / concepts / events 页面
4. 更新 `wiki/timeline.md`
5. 更新 `wiki/domains/<domain>.md`
6. 评估 my-thinking
7. 更新 `wiki/index.md`
8. 追加 `wiki/log.md`

### 回答 query
1. 先读 `wiki/domains/<domain>.md` 或 `wiki/index.md` 定位相关页面
2. 读相关页面综合回答，引用 wiki 页面
3. 非平凡回答 → 询问是否存为 `wiki/queries/<slug>.md`
4. 追加 `wiki/log.md`

### Lint 健康检查
1. 扫描断链、孤立页面、缺失反向链接
2. 检查矛盾（`[!WARNING]` 是否完整）
3. 识别超过 6 个月的 `[!AS-OF]` 声明
4. 列出 Missing Pages 中长期未创建的页面
5. 检查各领域 hub 页是否过时
6. 追加 `wiki/log.md`

### 更新个人思考
新 ingest 内容与 `wiki/my-thinking/` 相关时：
1. 指出哪些观点被支持/挑战/修正
2. **追加**新条目（不删旧版本）
3. 用 `> [!MY-TAKE]` 标记最新立场

---

## Index 格式

`wiki/index.md` 分两部分：**按类型**浏览 + **按领域**浏览。

```markdown
# 主目录

## 按类型浏览
### Papers | Sources | People | Entities | Concepts | Events | My Thinking | Queries

## 按领域浏览
### AI Research
### [其他领域]

## Missing Pages
```

---

## Log 格式

```
## [YYYY-MM-DD] <operation> | <title>
<1–3行说明>
```

操作类型：`ingest` | `query` | `lint` | `note` | `thinking`

只追加，不修改历史。快速查看：`grep "^## \[" wiki/log.md | tail -10`

---

## AI 研究领域特有约定

### 时效性
- 状态性描述加 `> [!AS-OF YYYY-MM]`
- Ingest 旧文章时，摘要顶部标注原始发布日期 vs ingest 日期的差异
- Lint 时优先检查超过 6 个月的时效性声明

### 论文 Ingest 额外记录
- 主要主张（便于后续引用）
- 方法论局限性
- 后续引用或反驳情况（如已知）
- Benchmark 数字（便于未来对比）

### 模型发布事件
在 `wiki/events/` 创建页面并记录：
- 基准分数（与前代对比）
- 能力跃迁
- 安全/对齐特性
- 商业影响

### 预测追踪
可验证预测 → 在对应页面设 `## 预测追踪` 节，定期更新结果。

### 矛盾处理
遇到对立叙事（加速主义 vs 末日论）：
- 不要中立和稀泥
- 在 `wiki/my-thinking/` 中记录对这种张力的理解
- 用 `> [!WARNING]` 标记具体矛盾，注明各方来源

---

## 会话提示

- 开始时：读此文件 → 读 `wiki/log.md` 最后 10 条 → 读 `wiki/index.md`
- 用户放入 `raw/` 的文件，默认视为需要 ingest
- 判断 paper vs source，选择对应格式和目录
- Ingest 时，优先广度（多触及相关页面）而非单页深度
- 每次 ingest 都评估是否需要更新 `wiki/my-thinking/`
- 每次 ingest 都更新对应领域的 `wiki/domains/<domain>.md`
- 知识库的价值随交叉链接的密度复利增长
