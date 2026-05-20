# Task Templates

当用户希望获得“怎么提问更顺手”的模板时，优先给出下面这些可直接复用的句式。

## Bug 修复

```text
使用 $eyu-claude-style-collab 先复现问题，再定位根因，给出最小修复，最后跑相关测试验证。
```

## 功能实现

```text
使用 $eyu-claude-style-collab 先阅读相关代码路径，按现有模式实现，不要过度重构，改完自测。
```

## Code Review

```text
使用 $eyu-claude-style-collab 只做代码审查，优先找 bug、回归、边界条件、测试缺口。先列 findings，再给总结。
```

## 重构

```text
使用 $eyu-claude-style-collab 目标是降低复杂度，不改变行为。分小步修改，每步都可验证。
```

## 建立最小上下文

```text
使用 $eyu-claude-style-collab 先建立最小必要上下文：读 README、相关模块入口、测试文件和当前 diff，再开始改。
```

## 复杂任务先校准

```text
使用 $eyu-claude-style-collab 先判断任务级别：简单改动直接做；跨模块、架构/API/schema 或高风险操作先给计划并等我确认。
```

## 方案讨论

```text
使用 $eyu-claude-style-collab 先给推荐方案和核心取舍，不要直接改代码；等我确认方向后再实施。
```

## 强制闭环

```text
使用 $eyu-claude-style-collab 不要只分析，直接改代码；如果遇到阻塞，再告诉我阻塞点。做完后请输出：1. 改了什么 2. 为什么这么改 3. 验证结果 4. 剩余风险
```
