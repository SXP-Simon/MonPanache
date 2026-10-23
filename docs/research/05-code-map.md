# 05 · 官方代码地图与环境准备

[返回研究总览](README.md)

## 1. 固定研究版本

| 项目 | 分支 | 本次读取的 commit | commit 作者日期（UTC） |
| --- | --- | --- | --- |
| seekdb | `2026-competition` | `76f871eb5a84b664d487b03b3412ce50194135b5` | 2026-10-14 |
| PowerContext | `2026-competition` | `9db1753434162c0aa7c9f1189a1722e617880a52` | 2026-09-29 |
| PowerContext 生态占位 | `2026-competition-ecosystem` | `d647275c308e09b7b623f322a26f5c4e85734fb0` | 见版本清单 |

分支会移动，阅读链接使用 commit 固定。日期是提交元数据，不代表正式赛题发布时间。仓库与版本见 [机器可读清单](sources.lock.json)，这份清单只记录研究证据，不是比赛依赖锁文件。

本次使用官方 GitHub 分支 API、递归目录树和原始文件下载进行只读核查，**没有完整 clone、构建或执行这两套系统**。官方同名分支存在，不等于已经确认平台最终指定基线。

## 2. seekdb 阅读地图

以下文件内容已读取；向量索引目录另做了路径核查。按“表达式 → 通用工具 → 网络客户端 → 测试”阅读，可避免在大仓库里漫游。

| 入口 | 看什么 | 核查发现 |
| --- | --- | --- |
| [ob_expr_ai_embed.cpp](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/src/sql/engine/expr/ob_expr_ai/ob_expr_ai_embed.cpp) | `calc_result_typeN`、`eval_ai_embed`、`cg_expr` | 类型推导、执行和代码生成分层；有 plan cache 版本 TODO |
| [ob_expr_ai_complete.cpp](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/src/sql/engine/expr/ob_expr_ai/ob_expr_ai_complete.cpp) | prompt 与模型完成结果的转换 | 不支持分支不能当已实现能力 |
| [ob_expr_ai_rerank.cpp](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/src/sql/engine/expr/ob_expr_ai/ob_expr_ai_rerank.cpp) | `eval_ai_rerank`、`batch_result_add_base`、结果合并 | 读取路径存在 20 条批次和索引偏移 |
| [ob_ai_func_utils.cpp](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/src/sql/engine/expr/ob_expr_ai/ob_ai_func_utils.cpp) | provider 请求／响应适配、embedding 解码、模型调用 | 已有多 provider 和批量相关路径 |
| [ob_ai_func_client.cpp](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/src/sql/engine/expr/ob_expr_ai/ob_ai_func_client.cpp) | `send_post`、`send_post_batch`、超时、重试、清理 | 可研究截止时间与部分失败，但本次未证明缺陷 |
| [ob_ai_func.cpp](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/src/sql/engine/expr/ob_expr_ai/ob_ai_func.cpp) | 表达式信息初始化／复制 | 配置信息生命周期入口 |
| [ai_prompt.test](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/tools/deploy/mysql_test/test_suite/ai_function/t/ai_prompt.test) | 上游 SQL 回归测试风格 | 可学习正常／错误用例结构，不代表覆盖全部模型调用 |
| [vector_index 目录](https://github.com/oceanbase/seekdb/tree/76f871eb5a84b664d487b03b3412ce50194135b5/src/observer/vector_index) | async task、scheduler、IVF cache、util | 目录存在；本次未完整追踪 ANN 核心调用链 |

开发文档入口：[开发者手册](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/docs/developer-guide/zh/README.md)、[工具链](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/docs/developer-guide/zh/toolchain.md)。手册还链接构建、GTest、mysqltest、调试和内存管理。后续按正式基线版本阅读具体步骤，不混用 master 文档。

## 3. PowerContext 阅读地图

| 入口 | 关键符号／内容 | 研究用途 |
| --- | --- | --- |
| [memory/service.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/artifacts/memory/service.py) | `MemoryService.search`、`_reranked_search_result`、`remember`、`forget`、`validate_citation` | 检索与记忆生命周期主入口 |
| [memory/reranking.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/artifacts/memory/reranking.py) | `MemoryReranker`、`LLMMemoryReranker`、`_normalize_ranks` | 利用现有重排接口，保持候选身份 |
| [artifacts/search.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/artifacts/search.py) | `AdmissionFloor`、文本分析、FTS admission | 查询分析和候选准入；不把全文匹配等同最终排序 |
| [persistence/memory_index.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/persistence/memory_index.py) | `MemoryIndex`、`CompositeMemoryIndex` | 持久化索引协议与组合 |
| [scope/search.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/scope/search.py) | `literal_contains` | 作用域发现，非 Memory 融合主流程 |
| [source_eligibility.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/source_eligibility.py) | `is_generation_eligible`、`require_source_eligible` | 生成证据与内部谱系来源边界 |
| [handoff/service.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/src/powercontext/builtin/artifacts/handoff/service.py) | `prepare`、`finalize`、`commit`、`continue_from` | 交接生命周期与证据验证 |
| [test_reranking.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/tests/builtin/artifacts/memory/test_reranking.py) | 重排边界测试 | 模仿隔离模型的单测方式 |
| [test_service.py](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/tests/builtin/artifacts/handoff/test_service.py) | Handoff service 测试 | 交接行为的现有测试入口 |

### RFC 的使用方法

已读取 [0028 Context Pack](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/docs/zh/rfcs/0028_context_pack.md)、[0080 Memory 重排](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/docs/zh/rfcs/0080_memory_search_reranking.md)、[1745 决策模型重排接口](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/docs/zh/rfcs/1745-decision-model-rerank-seam.md)。RFC 解释设计意图，但其中有未来方向；对每项能力还需找实现、装配入口与测试。尤其不能把“有第二种重排策略提案”写成“已经证明质量更好”。

## 4. 生态分支实际包含什么

[固定 commit 的生态分支](https://github.com/oceanbase/powercontext/tree/d647275c308e09b7b623f322a26f5c4e85734fb0) 本次递归目录只见 `dify/.gitkeep`、`gaode/.gitkeep`、`minimax/.gitkeep`、`qoder/.gitkeep`、`stepfun/.gitkeep`。这是占位结构；不能推断其他伙伴不参赛，也不能把五个目录当完整七题。

## 5. 你的 Windows 环境如何准备

研究版本 seekdb 工具链文档已有 Windows 11 x64 的 `build.ps1` 路线，也有 Linux／WSL 路线；不能沿用“seekdb 完全不能在 Windows 编译”的旧印象。PowerContext README 则将 Windows 标为实验性，Python 版本要求为 3.11 或以上。[seekdb 工具链](https://github.com/oceanbase/seekdb/blob/76f871eb5a84b664d487b03b3412ce50194135b5/docs/developer-guide/zh/toolchain.md) · [PowerContext README](https://github.com/oceanbase/powercontext/blob/9db1753434162c0aa7c9f1189a1722e617880a52/README.md)

**建议：** 等正式测试机环境明确后，优先让本地测试与它一致。如果平台使用 Linux，可用 WSL／独立 Linux 开发环境减少差异；这是一项工程选择，非比赛规则。当前资料仓库只保存笔记，不宜直接混入大体积构建产物。

首次准备应记录 OS、架构、CPU／RAM、磁盘、编译器、Python、依赖锁、数据库模式、模型配置和 commit。先运行原始基线再改代码；首次失败必须能区分网络下载、依赖、编译、启动和功能错误。

以下只是后续获取研究快照的示例，**本次未执行，且正式题面指定版本优先**：

```powershell
git clone --branch 2026-competition --single-branch https://github.com/oceanbase/seekdb.git seekdb-research
git -C seekdb-research switch --detach 76f871eb5a84b664d487b03b3412ce50194135b5

git clone --branch 2026-competition --single-branch https://github.com/oceanbase/powercontext.git powercontext-research
git -C powercontext-research switch --detach 9db1753434162c0aa7c9f1189a1722e617880a52
```

真正开始实现前从指定基线创建自己的功能分支，并按该版本文档构建。不要仅凭本报告的示意代码宣称构建已经验证。
