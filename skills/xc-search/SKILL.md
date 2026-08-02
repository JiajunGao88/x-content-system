---
name: xc-search
description: |
  个人内容层：检索素材库。在我自己的素材库 + dbskill 知识库（4176 条原子 + Skill 知识包）里搜相关概念/金句/爆款结构/已发布内容，找到就先建议复用。
  触发方式：/xc-search、/找素材、/检索素材、「有没有写过」「相关内容」「素材库里有没有」
  Personal content layer: search my own asset library plus the dbskill knowledge base (4176 atoms + skill packs) for reusable concepts, lines, viral structures, and published posts.
  Trigger: /xc-search, "找素材", "have I written about this"
---

# xc-search：检索素材库（个人内容层 + dbskill 知识库融合）

> 属于个人内容层（`xc-*`）。本 skill 的最大升级：检索范围从"我自己的素材库"扩到"我的素材库 ＋ dontbesilent 的整个知识库"。

## 触发条件
用户说"找素材"、"检索素材"、"有没有写过"、"相关内容"等。

## 核心规则
- 按优先级检索；先我的，再他的。
- 返回要具体，展示内容摘要，不要只说"找到了"。
- 没找到明确说"素材库中没有相关内容"，并给新写角度 + 写完后入库建议。

## 工作流程

1. 解析检索意图（关键词/主题/情绪）。
2. 依次检索：

| 优先级 | 目录 | 检索内容 |
|--------|------|----------|
| 1 | `02-内容素材库/核心概念库/` | 我的理论框架、方法论 |
| 2 | `02-内容素材库/金句库/` | 我的高质量表达 |
| 3 | `02-内容素材库/爆款推文库/` | 我已验证的推文结构 |
| 4 | `01-内容生产/已发布/` | 我已发布的内容 |
| 5 | `02-内容素材库/灵感碎片/` | 我的未整理原始素材 |
| 6 | **`知识库/原子库/atoms.jsonl`** | **dbskill 的 4176 条结构化知识点**，按 `topics`/`skills`/`type` 过滤（type 取 case/anti-pattern 可只看真实案例）|
| 7 | **`知识库/Skill知识包/`** | **dbskill 方法论文档**，内容创作相关重点看 `content_内容创作方法论.md`、`content_平台特性与案例.md`；概念解构看 `deconstruct_*` |
| 8 | `知识库/高频概念词典.md` | dbskill 高频概念速查 |

> 检索原子库可用命令辅助，如（PowerShell）：`Select-String -Path 知识库/原子库/atoms.jsonl -Pattern "关键词"`，或按 topics 过滤后读 knowledge/original 字段。

3. 返回格式：
```
📂 找到 X 条相关素材：

1. [来源：我的素材库 / dbskill 知识库] [文件/原子 ID]
   摘要：[相关段落或 knowledge 字段]
   复用建议：[怎么用到当前需求]
```

4. 没找到：
```
素材库中没有直接相关的内容。
建议：可以从 [角度] 新写；写完后入库到 [具体目录]（用 /xc-save）。
```

## 注意事项
- 我的素材库代表我的人设和语感，优先级高于他的通用知识库——他的知识库用于补充论据、案例、方法，但**表达和判断要回到我的宪法**。

## 与 dbskill 衔接
- 检索发现这是个值得长期工程化的大主题 → `/dbs-content-system`。
- 检索后要写 → `/xc-write`。
