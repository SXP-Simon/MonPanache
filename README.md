# MonPanache

第六届 OceanBase 数据库大赛的备赛资料与学习笔记。资料核对日期：**2026-10-23（北京时间）**。

## 最新研究报告

**[赛题与优化研究总览](docs/research/README.md)**：8 篇专题覆盖赛制、seekdb、PowerContext、七家现行生态方向、代码入口、评测方法、选题计划和来源记录。

10 月 23 日发现官网题量由 **11／11／8 更新为 12／11／7**，总量仍为 30 题、620 分。原力灵机有历史培训材料，但不在当前七家生态名单中；详见[差异记录](docs/research/08-evidence.md)。

## 先看这几件事

- 本届主题是 **数据库 + AI**，初赛共 **30 题、620 分**：seekdb 12 题、PowerContext 11 题、AI 生态 7 题。
- 官网当前赛程：报名截至 **2026-10-26**；初赛 **2026-10-26 至 2026-11-18**；决赛、答辩在 **12 月中旬**。具体截止时刻待正式通知。
- 每队 **1–3 人**；往届全国 20 强选手不得报名本届；本届开放 AI Coding。
- **MiniOB 用来补数据库基础、练习往届题。不要将其旧赛制直接套用于第六届。**

以上赛事信息来自[本届官网](https://open.oceanbase.com/competition?activityCode=4924143&officerId=5045)“大赛介绍 / 赛题说明 / 参赛时间”。培训转录里存在旧日期和识别错误，见[最新来源与差异记录](docs/research/08-evidence.md)。

## 阅读入口

| 想解决的问题 | 去哪里 |
| --- | --- |
| 比什么、什么时候比、现在该做什么？ | [01 · 比赛速览](docs/01-competition-overview.md) |
| seekdb、PowerContext 与生态培训方向分别做什么？ | [02 · 赛题方向与选题](docs/02-tracks-and-topics.md) |
| MiniOB 和本届有什么关系，怎么入门？ | [03 · MiniOB 学习地图](docs/03-miniob-learning-map.md) |
| 20 份材料怎么读，报名截止前怎么安排？ | [04 · 阅读路线与行动清单](docs/04-reading-plan.md) |
| 哪些已核实，哪些只是培训预告？ | [05 · 来源、冲突与待确认项](docs/05-sources-and-open-questions.md) |
| 找原始转录、字幕时间戳 | [材料目录与逐讲导读](materials/README.md) |

## 仓库结构与分支

```text
README.md                  阅读导航
docs/                      整理后的中文指南
  research/                10/23 深入研究、代码地图与评测模板
materials/
  README.md                20 讲导读与原文链接
  manifest.json            40 个文本文件的大小、SHA-256 和字幕时长
  transcripts/txt/         原始 TXT（部分为精简稿）
  transcripts/srt/         原始 SRT（含时间戳）
```

- `main` 是主分支，目前保留初始化占位 README。
- `docs/competition-guide` 保存初版资料整理。
- `research/competition-topics-2026` 承载本次深入研究，从资料分支创建，尚未合并到 `main`。
- 此分支是备赛资料；尚未部署数据库、实现赛题或验证编译命令。后续实验应记录具体仓库、分支和 commit。

## 官方入口

- [第六届比赛官网](https://open.oceanbase.com/competition?activityCode=4924143&officerId=5045)
- [seekdb 源码](https://github.com/oceanbase/seekdb)
- [PowerContext 源码](https://github.com/oceanbase/powercontext) · [文档](https://powercontext.oceanbase.io/en/docs/)
- [MiniOB 源码](https://github.com/oceanbase/miniob) · [文档](https://oceanbase.github.io/miniob/)

转录材料保留原文件名与内容，不代表已经逐字校正；原始课程与材料权利归原权利人所有。整理笔记中的学习顺序、选题判断和自测建议均不是官方评分细则。
