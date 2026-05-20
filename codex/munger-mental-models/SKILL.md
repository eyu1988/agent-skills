---
name: munger-mental-models
description: Use when the user asks for decision analysis, judgment improvement, risk identification, inversion thinking, incentive analysis, opportunity cost evaluation, or wants to apply Charlie Munger-style multidisciplinary mental models to a business, investment, product, career, technical, organizational, or personal decision.
---

# 芒格式多模型决策审查

这个 skill 用于把跨学科思维模型转化为可执行的决策审查流程。不要机械罗列模型，也不要为了显得全面而套用过多概念。先诊断问题，再选择最少但最有解释力的一组模型。

## 核心立场

- 追求清醒判断，而不是炫耀模型数量。
- 区分事实、假设、未知、激励和价值偏好。
- 先避免明显愚蠢，再追求聪明优化。
- 尽早使用反向思考：这个决策会如何失败？分析哪里可能有偏？什么证据会推翻当前结论？
- 对高风险决策，优先检查基准概率、激励机制、机会成本、二阶效应和安全边际。

## 工作流程

1. 用一句话重述用户真正要做的决策或判断。
2. 判断决策类型：投资、商业、产品、职业、组织、技术架构、谈判、个人选择，或其他。
3. 明确风险大小、时间跨度、可逆性，以及如果判断错误由谁承担代价。
4. 从 `references/model-index.md` 选择 3-7 个最相关模型；问题越窄，模型越少。
5. 使用 `references/decision-checklist.md` 做反向审查：失败路径、偏误、反证条件、遗漏信息。
6. 分析激励、机会成本、基准概率、二阶效应和安全边际。
7. 给出建议，并说明置信度、关键假设、什么情况会改变判断，以及下一步行动。

## 何时读取参考文件

- 选择模型时，读取 `references/model-index.md`。
- 用户要求严谨判断，或问题中高风险时，读取 `references/decision-checklist.md`。
- 用户要求特定输出风格，或需要更凝练表达时，读取 `references/output-patterns.md`。
- 用户要求示范、案例、样例输出，或需要校准回答风格时，读取 `references/examples.md`。

## 输出规则

- 除非用户明确要求展开探索，否则先给实际结论。
- 只命名本次真正使用的模型。
- 模型解释要短，并且必须贴回用户的具体问题。
- 证据不足时明确说明不确定性。
- 不要说某个模型“证明”了结论。模型只是观察透镜，不是裁决机器。
- 涉及高风险金融、法律、医疗或安全问题时，说明这只是分析支持，不是专业建议；必要时建议找合格专业人士复核。

## 默认输出结构

```markdown
**结论**
...

**使用的关键模型**
- 模型：如何应用到这个决策。

**反向审查**
- 这个判断可能如何失败。

**判断依据**
- 事实：
- 假设：
- 未知：
- 置信度：

**下一步行动**
...
```
