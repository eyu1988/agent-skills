---
name: "larktime-tech-debt-reporter"
description: "面向 LarkTime/Calendar iOS 模块生成可落库的技术债盘点报告。用户要求分析某个子模块技术债、标注 harness 接入关联度、输出 Obsidian 友好 Markdown、沉淀治理队列或评估 harness readiness 时触发。"
---

# LarkTime 技术债报告生成

## 触发条件

- 用户要求盘点 LarkTime、Calendar 或其子模块的技术债。
- 用户要求标注与 harness 接入的关联度、阻塞点、readiness 或自动化验证风险。
- 用户要求生成可落库 Markdown、Obsidian 阅读友好的技术债报告。
- 用户要求从某个子目录开始分析，例如 `Detail(MVVM)`、`MetaController`、`ComponentSpace`。

## 输入

- 代码范围：模块目录或子模块目录。
- 输出路径：用户指定路径；若未指定，使用仓库相对路径 `doc/technical_debt/`。
- 分析重点：harness 接入、稳定性、可维护性、测试缺口、架构治理、Owner 推进等。

## 输出

- 一份 Markdown 技术债报告，结构参考 `references/report-template.md`。
- 报告必须 Obsidian 阅读模式友好：frontmatter、清晰标题层级、callout、表格、内部链接。
- 报告中的代码位置使用仓库相对路径和行号，不写本机绝对路径。

## 工作流程

### 1. 明确范围与落库规则

1. 确认分析目录、模块边界和首批聚焦范围。
2. 若用户指定输出路径，按用户路径落库；若未指定，使用仓库相对路径 `doc/technical_debt/`。
3. 报告内不得写本机绝对路径；路径统一写为仓库相对路径或占位变量，如 `<repo>/doc/technical_debt/`。

### 2. 收集证据

优先使用只读命令：

- `git rev-parse HEAD`：记录 `evidence_commit` 和 `last_verified_commit`。
- `rg --files <scope>`：统计文件范围。
- `wc -l`：估算代码规模。
- `rg`：搜索 ViewModel、Controller、Builder、Reformer、Service、Legacy、Test、FG、AppConfig、Rx/Combine、debug 代码等风险点。
- `git log --since='3 months ago' -- <scope>`：统计 churn 和高频变更文件。
- `find` 或 `rg --files`：定位 OWNERS、测试目录、已有测试文件。

证据必须可复核：

- 每项技术债至少给出一个 `文件:行号` 证据。
- 对推断性结论标注“基于代码结构推断”或“需 Owner 校准”。
- 对未获取到的数据明确写“未接入线上 bug/crash/flaky 数据”。

### 3. 识别技术债

按以下维度扫描：

- 架构边界：ViewModel 是否过大，是否混合 UI、网络、状态、业务规则。
- 数据可控性：是否能离线 fixture 化，是否强依赖在线 API、容器、全局状态。
- 可观测性：是否有 snapshot、idle、effect、route、toast 等可断言出口。
- 测试缺口：是否有被注释的旧测试、缺少矩阵测试、缺少 fake loader。
- 入口矩阵：scene/options/payload 是否可枚举、是否存在弱类型组合。
- 并发与确定性：Rx/Combine/DispatchQueue/全局写入是否影响 harness 稳定性。
- 维护噪声：debug print、临时代码、重复映射、手写缓存表。

### 4. 标注 harness 关联度

使用四级分级，不混用“高/中/低”与工程分级；如用户明确要求高/中/低，可在表格中额外加一列映射。

| 分级 | 含义 |
| --- | --- |
| Blocker | 不处理会直接阻碍首批 harness 接入，例如无法离线构造页面、无法确定组件输出。 |
| Stabilizer | 不处理也能接入，但会导致 case flaky、等待条件脆弱或并发污染。 |
| Coverage | 主要影响覆盖率扩展、局部动作验证或长期维护成本。 |
| Low | 主要是日志噪声、临时代码、维护体验问题。 |

### 5. 输出报告

报告优先采用以下二级结构：

1. `决策摘要`
2. `范围与基线`
3. `分析摘要`
4. `技术债清单`
5. `治理计划`
6. `附录`

核心要求：

- `决策摘要` 面向 Owner，必须能在 2 分钟内读完。
- `技术债清单` 面向开发，必须包含证据、影响、建议、harness 切入点、首个 PR 范围、验收标准、迁移风险、verification plan。
- `治理计划` 面向落地，必须给出 PR 队列、验收信号和回滚策略。
- 避免重复章节：不要同时保留多份优先级总览、拆解路线、Done Definition 和 Rollback Plan；能合并成一张表就合并。

## 质量门禁

- 标题层级清晰：`决策摘要` 下放 `一页结论 / Owner 只需确认 / 里程碑计划 / 明确不做`。
- 报告不得出现本机绝对路径。
- 每项技术债有仓库相对路径证据和 harness 分级。
- P0/Blocker 项必须有首个 PR 范围和测试验证方式。
- 治理队列必须能拆成小 PR，且每项有回滚策略。
- 明确列出仍需 Owner 确认的信息，例如 DRI、CI job、线上 bug/crash/flaky 数据。

## 子代理评估

仅当用户明确要求“subagent 评估/打分/复核”时再启动子代理。给子代理的任务应只包含报告路径、评分标准和期望输出，不泄露预设答案。

## references

- `references/report-template.md` — 技术债报告推荐结构与字段。
