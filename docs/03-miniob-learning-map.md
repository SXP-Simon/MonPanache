# 03 · MiniOB 学习地图

## MiniOB 在这份材料里的位置

MiniOB 是用于学习数据库实现的 C++ 项目，适合把理论连接到可运行代码。其 README 与文档包含往届 OceanBase 初赛说明，但**本届官网已明确以 seekdb、PowerContext 与 AI 生态设置题目**。MiniOB 是基础学习支线，不是已经确认的第六届提交基线。[MiniOB 官方介绍](https://github.com/oceanbase/miniob) · [本届赛题说明](https://open.oceanbase.com/competition?activityCode=4924143&officerId=5045#instruction)

| 项目 | 本次应如何使用 |
| --- | --- |
| MonPanache | 保存资料、学习笔记、选题依据与实验记录 |
| MiniOB | 理解 SQL 执行和存储机制，练习往届题 |
| seekdb | 本届数据库方向的重点项目；使用正式指定版本做题 |
| PowerContext | 本届上下文方向的重点项目；使用正式指定版本做题 |

不要在尚未确定基线时把三个上游源码直接混入此资料仓库。可以在独立目录做实验；本仓库的 `local/` 已忽略，适合临时存放本机实验。

## 先跟踪一条 SQL

```text
客户端输入 SQL
    ↓
解析：这条语句的结构是什么？
    ↓
语义检查：表、字段、类型是否合法？
    ↓
计划与优化：用哪些步骤完成查询？
    ↓
执行：扫描、过滤、投影等步骤如何得到结果？
    ↓
存储：记录、页、索引、事务和日志如何配合？
```

先用一张小表做 `CREATE / INSERT / SELECT`，再选择过滤或索引查询追踪。上游会演进，以下目录是阅读入口；文件名与职责应以实际 checkout 为准：

| 入口 | 阅读时的问题 |
| --- | --- |
| `src/observer/sql/` | 从解析、语义到计划执行，结果如何传递？ |
| `src/observer/storage/` | 记录与索引如何组织，事务和恢复如何协作？ |
| `src/observer/net/`、`src/observer/session/` | 请求如何进入数据库，会话状态如何保存？ |
| `test/`、`unittest/` | 哪些测试说明了可接受的行为与边界？ |
| `docs/` | 设计文档与当前实现是否一致？ |

这是建议的阅读问题，不要求先读完整个仓库才开始动手。

## Windows 用户的环境路线

建议在 Linux 环境（例如 WSL2、Linux 虚拟机或合适的 Docker 开发环境）编译；这是本指南的环境建议。本次没有安装环境、克隆 MiniOB 或运行下面命令。

官方编译文档列出的基础要求：CMake ≥ 3.13、支持 C++20 的编译器（页面列举 GCC 11 以上 / Clang 14 以上）、flex 2.5+、bison 3.7+，以及 make 等工具。[编译文档](https://oceanbase.github.io/miniob/how_to_build/)

下面是依据官方文档整理的 **Bash 示例**，在准备好的 Linux 环境和独立学习目录中执行，不是在 Windows PowerShell 中直接执行：

```bash
# clone 时仅为这个学习仓库关闭 CRLF 转换
git clone -c core.autocrlf=false https://github.com/oceanbase/miniob.git miniob-study
cd miniob-study
git rev-parse HEAD              # 记录本次使用的 commit
bash build.sh init              # 首次准备依赖；官方预配环境可能可跳过
bash build.sh                   # 默认 Debug 构建
cd build_debug                 # 以实际生成的构建目录为准
./bin/observer -f ../etc/observer.ini -P cli
```

官方运行页说明 `observer` 是服务端，`obclient` 是配套客户端；`-P cli` 可直接在命令行执行 SQL。[运行文档](https://oceanbase.github.io/miniob/how_to_run/)

```sql
CREATE TABLE study_item (id INT, score INT);
INSERT INTO study_item VALUES (1, 90);
SELECT * FROM study_item;
SELECT score FROM study_item WHERE id = 1;
```

示例目标是验证基础闭环；结果应返回插入的记录。本次未实际验证此 SQL 在某个固定 commit 上的输出格式。

## 按需读官方文档

1. [文档首页](https://oceanbase.github.io/miniob/)：先看“设计文档 → MiniOB 架构”。
2. [编译](https://oceanbase.github.io/miniob/how_to_build/)与[运行](https://oceanbase.github.io/miniob/how_to_run/)：先获得可重复运行的环境。
3. 首页“SQL 词法语法分析 / SQL 表达式”：对应语法、类型和函数学习。
4. 首页“存储实现 / B+Tree / 事务模块 / 持久化”：对应存储与一致性学习。
5. 首页“训练营平台使用说明 / MiniOB 集成测试”：用于基础训练；其中仓库权限、账号和提交约定不能自动套用到本届。

## 一个合格的基础学习记录

- 上游仓库、分支与 commit。
- 环境版本和实际执行命令。
- 一条 SQL 的调用路径、关键数据结构。
- 一处行为修改及其验证结果。
- 遇到的问题、失败日志摘要与解决方式。

如果主要目标是本届参赛，达到“能运行、能调试、能解释一条请求”的程度就可以回到 seekdb / PowerContext。不要把先做完所有 MiniOB 历年题设为参赛前置条件。
