# loop-superpowers — Autonomous Mini-Loop Skills for Claude Code

[![Version](https://img.shields.io/badge/version-0.1.1-blue)](https://github.com/PerryLink/loop-superpowers)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](./LICENSE)

[English](#english) | [中文](#chinese)

<a id="english"></a>

## English

loop-superpowers is a collection of autonomous mini-loop skills for Claude Code, extending the [Superpowers](https://github.com/PerryLink/superpowers) plugin with closed-loop autonomous task execution.

## Features

- 7 autonomous mini-loop skills — brainstorming, planning, execution, debugging, TDD, verification, pipeline orchestration
- One skill = one closed loop — built-in turn-limit protection (3-8 turns), stop signals, and compliance self-audit
- Natural-language Phase Contracts — `<<<PHASE_CONTRACT>>>` blocks define expected_outputs, banned_behaviors, stop_signal, decision_rules
- Compliance audit trail — every turn self-reports B1-B6 violation checks to `compliance-log.md`
- Pipeline orchestrator — `/loop-pipeline` chains all 6 skills in sequence with data handoff and gate evaluation
- Zero compiled code — pure Markdown + YAML frontmatter, no build step, no `package.json`, no CI required
- Designed for Claude Code Plugin system — auto-registered via `plugin.json`, compatible with Claude Code >= 2.1.0

## Quick Start

```bash
# 1. Install Superpowers first (required dependency)
# Claude Code: /plugin install superpowers

# 2. Clone loop-superpowers
git clone https://github.com/PerryLink/loop-superpowers.git

# 3. Copy skills to your Claude Code skills directory
cp -r loop-superpowers/.claude/skills/* ~/.claude/skills/

# 4. Restart Claude Code — all 7 slash commands auto-register
# Try: /loop-brainstorming "How to implement rate limiting for a REST API"
# Try: /loop-tdd --input artifacts/task-plan.json
# Try: /loop-pipeline --goal "Build a CLI todo app"
```

Requirements: Claude Code >= 2.1.0, Superpowers plugin >= 1.0.0 installed.

## FAQ

### Q: loop-superpowers has no code — how does the loop work?
A: Each SKILL.md embeds a natural-language Phase Contract that acts as a behavioral boundary for Claude Code. The agent self-governs within defined turn limits and stop conditions — the "loop" emerges from this self-governance rather than compiled code.

### Q: Why no compiled code or tests?
A: This is by design. loop-superpowers is a pure configuration/skill project — its "code" is natural-language instructions (SKILL.md) and its "runtime" is Claude Code itself.

### Q: Can I chain multiple skills together?
A: Yes, use `/loop-pipeline` for automated chaining through all 6 skills. Or chain manually: run `/loop-brainstorming` to produce `03-solution.md`, then pass it as `--input` to `/loop-planning`, then pass `task-plan.json` to `/loop-execution`, and so on. Each skill's Appendix E documents upstream/downstream dependencies.

### Q: What happens if a skill gets stuck?
A: Every skill has built-in protection: turn-limit protection (3-8 turns, skill-dependent) prevents infinite loops; `banned_behaviors` enforcement prevents dangerous actions; Error Handling Matrices define recovery paths for 5-7 failure scenarios per skill; the pipeline orchestrator detects stalled stages; all decisions and audits are logged for traceability.

## Related Projects

- [loop-opencode](https://github.com/PerryLink/loop-opencode) — closed-loop driver for OpenCode CLI
- [loop-codex](https://github.com/PerryLink/loop-codex) — dual-channel (JSON-RPC + CDP) driver for Codex Desktop
- [loop-copilot](https://github.com/PerryLink/loop-copilot) — closed-loop driver for GitHub Copilot SDK
- [loop-cursor](https://github.com/PerryLink/loop-cursor) — closed-loop driver for Cursor IDE SDK
- [loop-deepseek](https://github.com/PerryLink/loop-deepseek) — self-built ReAct agent loop for DeepSeek API
- [loop-ollama](https://github.com/PerryLink/loop-ollama) — self-built ReAct agent loop for local Ollama models
- [loop-antigravity](https://github.com/PerryLink/loop-antigravity) — closed-loop driver for Google Antigravity / Gemini
- [loop-openclaw](https://github.com/PerryLink/loop-openclaw) — multi-agent loop config generator for OpenClaw Gateway

## License

Apache License 2.0 — see [LICENSE](./LICENSE) for full text.

---

<a id="chinese"></a>

## 中文

[English](#english) | **中文**

# loop-superpowers —— Claude Code 自主迷你循环技能集

> **loop-superpowers 是纯 Skill 集合项目 —— 7 个 Claude Code Skill，零编译二进制，零运行时依赖。**
> 把 Superpowers 的每个技能变成自主 mini-loop——选择技能，设定目标，自动跑到底。

loop-superpowers 是一个 Claude Code 自主迷你循环技能集合，为 [Superpowers](https://github.com/PerryLink/superpowers) 插件扩展闭环自主任务执行能力。

## 特性

- **7 个自主迷你循环技能** —— 头脑风暴、规划、执行、调试、TDD、验证、流水线编排
- **一个技能 = 一个闭环** —— 内建轮次限制保护（3-8 轮）、停止信号和合规自审
- **自然语言 Phase Contract** —— `<<<PHASE_CONTRACT>>>` 块定义 expected_outputs、banned_behaviors、stop_signal、decision_rules
- **合规审计追踪** —— 每轮自动报告 B1-B6 违规检查到 `compliance-log.md`
- **流水线编排器** —— `/loop-pipeline` 按顺序串联全部 6 个技能，含数据传递和闸门评估
- **零编译代码** —— 纯 Markdown + YAML 前置元数据，无构建步骤，无 `package.json`，无需 CI
- **专为 Claude Code Plugin 系统设计** —— 通过 `plugin.json` 自动注册，兼容 Claude Code >= 2.1.0

## 快速开始

```bash
# 1. 先安装 Superpowers（必要依赖）
# Claude Code: /plugin install superpowers

# 2. 克隆 loop-superpowers
git clone https://github.com/PerryLink/loop-superpowers.git

# 3. 复制技能到 Claude Code 技能目录
cp -r loop-superpowers/.claude/skills/* ~/.claude/skills/

# 4. 重启 Claude Code —— 全部 7 个斜杠命令自动注册
# 试试: /loop-brainstorming "如何为 REST API 实现速率限制"
# 试试: /loop-tdd --input artifacts/task-plan.json
# 试试: /loop-pipeline --goal "构建一个 CLI 待办事项应用"
```

依赖要求：Claude Code >= 2.1.0，Superpowers 插件 >= 1.0.0 已安装。

## 常见问题

### Q：loop-superpowers 没有代码 —— 循环如何工作？
A：每个 SKILL.md 嵌入了自然语言 Phase Contract，作为 Claude Code 的行为边界。Agent 在定义的轮次限制和停止条件内自我治理 —— "循环"是从这种自我治理中涌现的，而非来自编译代码。

### Q：为什么没有编译代码或测试？
A：这是有意为之。loop-superpowers 是纯配置/技能项目 —— 它的"代码"是自然语言指令（SKILL.md），"运行时"是 Claude Code 本身。

### Q：可以串联多个技能吗？
A：可以，使用 `/loop-pipeline` 自动化串联全部 6 个技能。或手动串联：运行 `/loop-brainstorming` 生成 `03-solution.md`，然后作为 `--input` 传递给 `/loop-planning`，再将 `task-plan.json` 传递给 `/loop-execution`，以此类推。每个技能的附录 E 记录了上下游依赖。

### Q：如果技能卡住了怎么办？
A：每个技能都有内置保护：轮次限制保护（3-8 轮，因技能而异）防止无限循环；`banned_behaviors` 执行防止危险操作；错误处理矩阵为每个技能定义了 5-7 种故障场景的恢复路径；流水线编排器检测停滞阶段；所有决策和审计都会记录以供追溯。

## 相关项目

- [loop-opencode](https://github.com/PerryLink/loop-opencode) —— OpenCode CLI 闭环驱动
- [loop-codex](https://github.com/PerryLink/loop-codex) —— Codex Desktop 双通道（JSON-RPC + CDP）驱动
- [loop-copilot](https://github.com/PerryLink/loop-copilot) —— GitHub Copilot SDK 闭环驱动
- [loop-cursor](https://github.com/PerryLink/loop-cursor) —— Cursor IDE SDK 闭环驱动
- [loop-deepseek](https://github.com/PerryLink/loop-deepseek) —— 面向 DeepSeek API 的自建 ReAct 代理循环
- [loop-ollama](https://github.com/PerryLink/loop-ollama) —— 面向本地 Ollama 模型的自建 ReAct 代理循环
- [loop-antigravity](https://github.com/PerryLink/loop-antigravity) —— Google Antigravity / Gemini 闭环驱动
- [loop-openclaw](https://github.com/PerryLink/loop-openclaw) —— OpenClaw Gateway 多代理循环配置生成器

## 许可证

Apache License 2.0 —— 详见 [LICENSE](./LICENSE) 文件。

Copyright 2026 Perry Link
