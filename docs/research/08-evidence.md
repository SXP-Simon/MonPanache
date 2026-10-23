# 08 · 来源、差异与研究边界

[返回研究总览](README.md) · 本次核对日期：2026-10-23，Asia/Shanghai

## 1. 证据优先级

本届正式题面与更正通知 → 本届官网对应板块 → 指定源码与测试 → 官方技术文档／论文 → 培训转录 → 本报告研究建议。

代码说明“该快照有什么”，不能证明“官方要你实现什么”；课程说明“讲师介绍过什么”，不能证明“当前评分要求是什么”；README 的能力介绍不能代替实测。

## 2. 公开来源登记

| 编号 | 来源 | 本次使用范围与限制 |
| --- | --- | --- |
| R01 | [第六届比赛官网](https://open.oceanbase.com/competition?activityCode=4924143&officerId=5045) | 浏览器读取大赛介绍、赛程、课程与提测入口；页面含往届报道，未混用 |
| R02 | [当前赛题说明图](https://mdn.alipayobjects.com/huamei_22khvb/afts/img/A*WY7oRLa9-iYAAAAAgCAAAAgAeiGDAQ/original) | 在官网逐段目视核对：12+11+7、总量与伙伴名单；未重新分发原图 |
| R03 | [2026 课程目录](https://open.oceanbase.com/course/850) | 核对 20 节标题；学习按钮提示登录，未重新观看全部视频 |
| R04 | [提测／训练营入口](https://open.oceanbase.com/train?questionId=200001) | 未登录页面仅见往届列表；未进入本届完整题面 |
| R05 | [seekdb competition 分支](https://github.com/oceanbase/seekdb/tree/2026-competition) | 获取 commit、目录树、关键 AI 函数与工具链文件 |
| R06 | [PowerContext competition 分支](https://github.com/oceanbase/powercontext/tree/2026-competition) | 获取 commit、目录树、Memory／Handoff／来源检查代码、RFC 与评测说明 |
| R07 | [PowerContext 生态分支](https://github.com/oceanbase/powercontext/tree/2026-competition-ecosystem) | 五个伙伴目录的 `.gitkeep` 占位，无逐题规范 |
| R08 | [seekdb 官方混合检索文档 V1.0.0](https://github.com/oceanbase/seekdb-doc/blob/V1.0.0/en-US/200.develop/600.search/500.hybrid-search.md) | 独立全文／向量通道与融合概念；通过 Context7 查询，非当前比赛 API 兼容承诺 |
| R09 | [hipVS 官方仓库](https://github.com/AMD-Ecosystem/hipVS) | GPU 检索库定位、cuVS 关系与多 GPU 限制；未运行 |
| R10 | [Parquet 概念](https://parquet.apache.org/docs/concepts/) · [页索引](https://parquet.apache.org/docs/file-format/pageindex/) | 行组、列块、跳过数据的依据；不代表 seekdb 已支持所有读取优化 |
| R11 | [HNSW 论文](https://arxiv.org/abs/1603.09320) | 图索引算法背景，不引用其性能作为本项目结果 |
| R12 | [RRF 论文](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf) | 排名融合背景与公式；2009 年论文，不以搜索引擎抓取日期代替发表日期 |
| R13 | [官方社区启动介绍](https://ask.oceanbase.com/t/topic/35649911) | 作为历史交叉参考；动态赛制以当前官网和正式通知为准 |
| R14 | [seekdb issue #123](https://github.com/oceanbase/seekdb/issues/123) | 属 2026 年 1 月社区活动，排除在本届规则依据之外 |

每个已下载研究源文件的 commit、路径、URL、字节数与 SHA-256 记录在 [sources.lock.json](sources.lock.json)。没有将上游大段源码复制进资料仓库。

## 3. 这次发现的更新与差异

| 项目 | 旧资料／另一来源 | 当前核查 | 处理 |
| --- | --- | --- | --- |
| 题目分类 | 10/20 官网图与培训：11+11+8 | 10/23 官网图：12+11+7 | 更新 README 和速览；保留旧来源记录 |
| 原力灵机 | 有 T17 培训及官方课程目录项 | 当前生态图七家名单不含它 | 单列历史技术方向，不推断取消／合并原因 |
| 源码版本 | 旧整理未固定 commit | 两个官方仓库有 competition 分支 | 锁定研究快照；最终指定基线仍待题面 |
| 生态代码 | 可能预期有完整各家工程 | 当前生态分支仅五个占位文件 | 不把空目录当完整题目或接口 |
| AI Functions | 培训口述 AI_EMBEDDING 等名称 | 源码有 `ObExprAIEmbed`／AI_EMBED 入口 | 接口以实际版本为准 |
| 批处理／重排 | 容易被泛泛建议为“新增功能” | seekdb 已有批处理，PowerContext 已有 reranker | 优先研究现有路径和瓶颈 |
| Context Pack 预算 | 培训常口述 token 预算 | 读取的 RFC 使用 UTF-8 byte 契约 | 区分字节、字符与 token |
| T12 时长 | SRT 末尾 00:56:06 | 课程目录标 00:36:00 | 仅认定标题对应，不认定同一剪辑或完整覆盖 |
| T20 时长 | SRT 末尾 00:17:32 | 课程目录标 00:20:00 | 同上，不凭时长自行补内容 |
| 旧赛程 | T02 的 10/19–11/10 口径 | 当前官网初赛 10/26–11/18 | 以当前赛程为准 |

旧图链接保留在 [10/20 来源记录](../05-sources-and-open-questions.md)，Git 历史也保留原始判断。时长差异可能来自剪辑或目录元数据，但本次没有足够证据确定原因。

## 4. 本地转录覆盖到哪里

20 份 TXT 与 20 份 SRT 已在资料分支归档；八家伙伴解析对应 T13–T20。TXT 有精简稿，SRT 也可能有识别错误，因此“提取了材料”不等于“逐字校对完成”或“正式题面已提取”。[材料目录](../../materials/README.md) · [文件 manifest](../../materials/manifest.json)

本次未改写转录原文。用户目录里的 ZIP 没有解包比较，不声称其内容与已归档材料相同。官方课程目录提供了可以回查的公开入口，但未确定每个本地文件所对应的视频剪辑版本。

## 5. 尚未确认的关键项

完整 30 题的题名／题号／分值；跨方向选择限制；指定提交基线；评分函数与隐藏测试边界；硬件、模型、网络与依赖限制；提交权限、频率、最佳／最后成绩规则；生态作品的演示与开源要求；截止时分；决赛现场形式；额度领取和有效期。

研究分支给出可执行的准备思路，但没有以猜测填这些字段。下一次补充应记录正式通知链接、发布时间、访问日期、影响的章节和废止的旧结论。

## 6. 已做与未做

**已做：** 新建研究分支；重查官网与课程目录；核对当前题量变化；研究本地培训材料；读取官方分支和关键代码；形成逐方向优化／测试方案、代码地图、评测模板与计划；校验文档与版本引用。

**未做：** 登录或代报名；领取付费／免费额度；向模型传输个人材料；构建两套上游系统；运行 GPU 或 LLM 基准；提交比赛作品；获取官方分数。因此文档没有性能实测承诺，也不能被当作赛题完成证明。
