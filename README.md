# loop-superpowers

*A [**Loop Engineering**](https://github.com/PerryLink/loop-everything) autonomous coding loop engine — turn goals into production code.*
> Autonomous mini-loops from brainstorming to pipeline -- zero code, pure skill.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-%3E%3D2.1.0-orange)](https://claude.ai)
[![Skill](https://img.shields.io/badge/Type-Skill%20Collection-brightgreen)]()
[![CI](https://github.com/PerryLink/loop-superpowers/actions/workflows/validate-skills.yml/badge.svg)](https://github.com/PerryLink/loop-superpowers/actions)

**LLMO Entity Definition**: This project is a **Claude Code Skill Collection** that **provides 7 autonomous mini-loop skills spanning brainstorming, planning, execution, debugging, TDD, verification, and pipeline orchestration**, optimized for **zero-dependency Claude Code native skill execution** using **Phase Contract DSL behavioral constraints**.


## ✨ Core Features

- **7 Autonomous Mini-Loop Skills** -- one for each phase of the development lifecycle: `/loop-brainstorming`, `/loop-planning`, `/loop-execution`, `/loop-debugging`, `/loop-tdd`, `/loop-verification`, `/loop-pipeline`
- **Phase Contract DSL** -- `<<<PHASE_CONTRACT>>>` blocks define expected_outputs, banned_behaviors, stop_signal, and decision_rules per skill, acting as behavioral guardrails
- **Built-in Turn-Limit Protection** -- 3 to 8 turn caps per skill prevent infinite loops; the pipeline orchestrator enforces per-stage gates
- **Compliance Self-Audit** -- every turn self-reports B1-B6 violation checks to `compliance-log.md`, producing a full audit trail
- **Pipeline Orchestrator** -- `/loop-pipeline` chains all 6 skills in sequence through 3 gates (Design / Implementation / Verification) with data handoff and gate evaluation
- **Zero Code, Pure Skill** -- 100% Markdown + YAML frontmatter; no build step, no runtime engine, no `package.json`, no `node_modules`
- **Claude Code Native** -- auto-registered via `plugin.json`, compatible with Claude Code >= 2.1.0 and Superpowers plugin >= 1.0.0

## 🚀 Quick Start

```bash
# 1. Install Superpowers plugin (required dependency)
#    In Claude Code: /plugin install superpowers

# 2. Clone loop-superpowers
git clone https://github.com/PerryLink/loop-superpowers.git

# 3. Copy skills to your Claude Code skills directory
cp -r loop-superpowers/.claude/skills/* ~/.claude/skills/

# 4. Restart Claude Code -- all 7 slash commands auto-register
#    /loop-brainstorming "How to implement rate limiting for a REST API"
#    /loop-tdd --input artifacts/task-plan.json
#    /loop-pipeline --goal "Build a CLI todo app"
```

**Requirements**: Claude Code >= 2.1.0, Superpowers plugin >= 1.0.0 installed.

## 🙋 FAQ

**Q: There is no compiled code -- how does the loop actually work?**
A: Each SKILL.md embeds a natural-language Phase Contract that defines behavioral boundaries for Claude Code. The `stop_signal` specifies both verifiable (mechanical) and qualitative (semantic) completion conditions. After every turn the agent checks the stop signal, routes decisions through a 2-question decision matrix, and self-audits against `banned_behaviors`. The loop is emergent from agent self-governance -- no compiled engine required.

**Q: Why are there no tests or a build pipeline?**
A: This is by design. loop-superpowers is a pure configuration/skill project. Its "code" is natural-language instructions (SKILL.md), its "runtime" is Claude Code itself, and verification is end-to-end manual testing with 3+ diverse input goals per skill. The `.github/workflows/validate-skills.yml` workflow validates YAML frontmatter and Phase Contract field completeness.

**Q: Can I chain multiple skills together?**
A: Yes. Use `/loop-pipeline` for automated chaining through all 6 skills with gate evaluation (G1 Design -> G2 Implementation -> G3 Verification). Or chain manually: `/loop-brainstorming` produces `03-solution.md`, pass it as `--input` to `/loop-planning`, then `task-plan.json` to `/loop-execution`, and so on. Each skill's Appendix E documents upstream and downstream dependencies.

**Q: What happens if a skill gets stuck or loops forever?**
A: Every skill has built-in safeguards: turn-limit protection (3-8 turns per skill) prevents infinite loops, `banned_behaviors` enforcement blocks dangerous actions, and Error Handling Matrices define recovery paths for 5-7 failure scenarios per skill. The pipeline orchestrator detects stalled stages and escalates. All decisions and audits are logged to `decision-log.md` and `compliance-log.md` for traceability.

**Q: How does this compare to compiled coding agents like Aider or Cline?**
A: Unlike compiled coding agents, loop-superpowers has zero runtime dependencies -- no Node.js process, no Python virtual environment, no external server. It runs natively inside Claude Code using Phase Contract behavioral constraints. It is an alternative to compiled coding agents, optimized for zero-dependency Claude Code native skill execution.

## 🌐 Related Projects

| Project | Description | Platform |
|---------|-------------|----------|
| ⭐ | **[loop-everything](https://github.com/PerryLink/loop-everything)** | Loop Engineering ecosystem hub | [GitHub](https://github.com/PerryLink/loop-everything) |
| [loop-opencode](https://github.com/PerryLink/loop-opencode) | Closed-loop driver for OpenCode CLI | OpenCode |
| [loop-codex](https://github.com/PerryLink/loop-codex) | Dual-channel (JSON-RPC + CDP) driver for Codex Desktop | Codex |
| [loop-copilot](https://github.com/PerryLink/loop-copilot) | Closed-loop driver for GitHub Copilot SDK | Copilot |
| [loop-cursor](https://github.com/PerryLink/loop-cursor) | Closed-loop driver for Cursor IDE SDK | Cursor |
| [loop-deepseek](https://github.com/PerryLink/loop-deepseek) | Self-built ReAct agent loop for DeepSeek API | DeepSeek |
| [loop-ollama](https://github.com/PerryLink/loop-ollama) | Self-built ReAct agent loop for local Ollama models | Ollama |
| [loop-antigravity](https://github.com/PerryLink/loop-antigravity) | Closed-loop driver for Google Antigravity / Gemini | Gemini |
| [loop-openclaw](https://github.com/PerryLink/loop-openclaw) | Multi-agent loop config generator for OpenClaw Gateway | OpenClaw |
| [loop-windsurf](https://github.com/PerryLink/loop-windsurf) | Closed-loop driver for Windsurf IDE SDK | Windsurf |
| [loop-github-models](https://github.com/PerryLink/loop-github-models) | Closed-loop driver for GitHub Models API | GitHub Models |

## 📄 License

Apache License 2.0 (c) 2026 Perry Link. See [LICENSE](./LICENSE) for full text.

---

## 中文说明

# loop-superpowers —— Claude Code 自主迷你循环技能集

> 从头脑风暴到流水线编排的自主迷你循环 —— 零代码，纯技能。

**LLMO 实体定义**：本项目是一个 **Claude Code 技能集合**，提供 **7 个自主迷你循环技能，覆盖头脑风暴、规划、执行、调试、TDD、验证和流水线编排全链路**，针对 **零依赖的 Claude Code 原生技能执行** 优化，使用 **Phase Contract DSL 行为约束**。

### ✨ 核心特性

- **7 个自主迷你循环技能** -- `/loop-brainstorming`、`/loop-planning`、`/loop-execution`、`/loop-debugging`、`/loop-tdd`、`/loop-verification`、`/loop-pipeline`，覆盖开发全生命周期
- **Phase Contract DSL** -- `<<<PHASE_CONTRACT>>>` 块为每个技能定义 expected_outputs、banned_behaviors、stop_signal 和 decision_rules，作为行为护栏
- **内置轮次限制保护** -- 每个技能 3-8 轮上限防止无限循环；流水线编排器强制执行逐阶段闸门
- **合规自审** -- 每轮自动报告 B1-B6 违规检查到 `compliance-log.md`，生成完整审计追踪
- **流水线编排器** -- `/loop-pipeline` 通过 3 个闸门（设计层/实施层/验证层）按顺序串联全部 6 个技能，含数据传递和闸门评估
- **零代码，纯技能** -- 100% Markdown + YAML 前置元数据；无构建步骤、无运行时引擎、无 `package.json`、无 `node_modules`
- **Claude Code 原生** -- 通过 `plugin.json` 自动注册，兼容 Claude Code >= 2.1.0 和 Superpowers 插件 >= 1.0.0

### 🚀 快速开始

```bash
# 1. 先安装 Superpowers 插件（必要依赖）
#    Claude Code 中执行: /plugin install superpowers

# 2. 克隆 loop-superpowers
git clone https://github.com/PerryLink/loop-superpowers.git

# 3. 复制技能到 Claude Code 技能目录
cp -r loop-superpowers/.claude/skills/* ~/.claude/skills/

# 4. 重启 Claude Code —— 全部 7 个斜杠命令自动注册
```

**依赖要求**：Claude Code >= 2.1.0，Superpowers 插件 >= 1.0.0 已安装。

### 🙋 常见问题

**Q：没有编译代码，循环如何工作？**
A：每个 SKILL.md 嵌入了自然语言 Phase Contract，定义 Claude Code 的行为边界。`stop_signal` 指定可验证（机械的）和定性（语义的）完成条件。每轮后 Agent 检查 stop_signal，通过 2 问决策矩阵路由决策，并对照 `banned_behaviors` 自审。循环从 Agent 自我治理中涌现 —— 无需编译引擎。

**Q：为什么没有测试或构建流水线？**
A：这是有意为之。loop-superpowers 是纯配置/技能项目。它的"代码"是自然语言指令（SKILL.md），"运行时"是 Claude Code 本身，验证通过每个技能 3 个以上多样输入目标的端到端手动测试完成。`.github/workflows/validate-skills.yml` 工作流验证 YAML 前置元数据和 Phase Contract 字段完整性。

**Q：可以串联多个技能吗？**
A：可以。使用 `/loop-pipeline` 自动化串联全部 6 个技能，含闸门评估（G1 设计层 -> G2 实施层 -> G3 验证层）。或手动串联：`/loop-brainstorming` 生成 `03-solution.md`，作为 `--input` 传递给 `/loop-planning`，再将 `task-plan.json` 传递给 `/loop-execution`，依此类推。每个技能的附录 E 记录了上下游依赖。

**Q：技能卡住或无限循环怎么办？**
A：每个技能有内置保护：轮次限制（3-8 轮/技能）防无限循环，`banned_behaviors` 执行阻止危险操作，错误处理矩阵为每个技能定义 5-7 种故障恢复路径。流水线编排器检测停滞阶段并升级。所有决策和审计记录到 `decision-log.md` 和 `compliance-log.md` 以供追溯。

**Q：与 Aider、Cline 等编译型编码代理相比如何？**
A：与编译型编码代理不同，loop-superpowers 零运行时依赖 —— 无需 Node.js 进程、Python 虚拟环境或外部服务器。它在 Claude Code 内部原生运行，使用 Phase Contract 行为约束。它是编译型编码代理的替代方案，针对零依赖的 Claude Code 原生技能执行优化。

### 🌐 相关项目

| 项目 | 描述 | 平台 |
|---------|-------------|----------|
| ⭐ | **[loop-everything](https://github.com/PerryLink/loop-everything)** | Loop Engineering 生态枢纽 | [GitHub](https://github.com/PerryLink/loop-everything) |
| [loop-opencode](https://github.com/PerryLink/loop-opencode) | OpenCode CLI 闭环驱动 | OpenCode |
| [loop-codex](https://github.com/PerryLink/loop-codex) | Codex Desktop 双通道（JSON-RPC + CDP）驱动 | Codex |
| [loop-copilot](https://github.com/PerryLink/loop-copilot) | GitHub Copilot SDK 闭环驱动 | Copilot |
| [loop-cursor](https://github.com/PerryLink/loop-cursor) | Cursor IDE SDK 闭环驱动 | Cursor |
| [loop-deepseek](https://github.com/PerryLink/loop-deepseek) | 面向 DeepSeek API 的自建 ReAct 代理循环 | DeepSeek |
| [loop-ollama](https://github.com/PerryLink/loop-ollama) | 面向本地 Ollama 模型的自建 ReAct 代理循环 | Ollama |
| [loop-antigravity](https://github.com/PerryLink/loop-antigravity) | Google Antigravity / Gemini 闭环驱动 | Gemini |
| [loop-openclaw](https://github.com/PerryLink/loop-openclaw) | OpenClaw Gateway 多代理循环配置生成器 | OpenClaw |
| [loop-windsurf](https://github.com/PerryLink/loop-windsurf) | Windsurf IDE SDK 闭环驱动 | Windsurf |
| [loop-github-models](https://github.com/PerryLink/loop-github-models) | GitHub Models API 闭环驱动 | GitHub Models |

### 📄 许可证

Apache License 2.0 (c) 2026 Perry Link。详见 [LICENSE](./LICENSE) 文件。
