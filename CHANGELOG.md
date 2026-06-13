# Changelog

All notable changes to the loop-superpowers plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.1.1] — 2026-06-13

### Security

- 新增 `SECURITY.md` — 安全策略文档，涵盖漏洞报告流程、安全模型（Skill指令注入防护）、依赖安全、配置安全最佳实践
- 新增 `.github/ISSUE_TEMPLATE/bug_report.md` — 标准化 Bug 报告模板，含 Phase Contract 相关分类
- 新增 `.github/ISSUE_TEMPLATE/skill_proposal.md` — Skill 提案模板，含 Phase Contract 草案格式
- 新增 `.github/PULL_REQUEST_TEMPLATE.md` — PR 模板，含 Skill 验证和测试清单

### Changed

- **CHANGELOG 结构重构** — 将单条目拆分为 Added / Changed / Fixed / Security 分类，遵循 Keep a Changelog 规范
- **SUFFICIENCY_DECLARATION.md** — 已知限制从 5 条扩展为更详细的局限性说明，含具体缓解措施
- **SKILL_VALIDATION.md** — 验证规则从 R1-R10 扩展至 R1-R12（新增 R11: 跨技能一致性检查、R12: 文档质量元验证）
- **CI workflow** — 增强 `validate-skills.yml`，添加对 `pipeline-config.json` 的 JSON 格式验证和 `plugin.json` 的 Schema 验证

### Added

- **.editorconfig** — 统一 Markdown/YAML/JSON 文件编码规范（UTF-8, LF, 缩进规则）

---

## [0.1.0] — 2026-06-13

### Added

- **7 loop skills** implementing autonomous mini-loop workflows on top of Superpowers base skills:
  - `loop-brainstorming` — Multi-turn creative exploration with convergence, producing structured solution documents. Max turns: 5. Phase contract enforces no premature implementation, structured output format, and verifiable completion criteria V1-V5.
  - `loop-planning` — Decompose requirements into execution plans with dependency ordering and checkpoint definition. Max turns: 3. Produces implementation_plan.md with per-task dependencies, estimated effort, and milestone checkpoints.
  - `loop-execution` — Drive implementation from a written plan with per-checkpoint review. Max turns: 8, checkpoints at turns 3, 5, 7. Banned behaviors include skipping checkpoints, modifying the plan without justification, and editing outside allowed file scope.
  - `loop-debugging` — Systematic bug investigation using the scientific method: hypothesis, test, observe, iterate. Max turns: 5. Requires documented hypothesis before any fix attempt; banned from making changes without evidence.
  - `loop-tdd` — Test-driven development loop: red (write failing test), green (implement), refactor. Max turns: 8. Enforces strict red-green-refactor cycle ordering with per-cycle artifact logging.
  - `loop-verification` — Validate that changes actually work before claiming completion. Max turns: 3. Requires running verification commands and confirming output before success claims; evidence before assertions always.
  - `loop-pipeline` — Orchestrator that chains the other 6 skills into a full end-to-end workflow (brainstorm -> plan -> execute -> debug -> tdd -> verify). Implements stage gates between phases with pipeline-level compliance audit logging.

### Design

- **Phase Contract Architecture** — Each skill operates under a self-enforcing `<<<PHASE_CONTRACT>>>` that defines:
  - Expected outputs (artifacts) with content requirements
  - Banned behaviors (5-7 per skill) with severity levels (fatal/high/medium/low)
  - Allowed file scope (restricted to per-skill artifacts directory)
  - Stop signals: verifiable (V1-V5 mechanical checks) + qualitative (Q1-Q4 semantic checks), composite AND rule — all must pass for normal completion
  - Decision rules: 2-question per-turn decision matrix (Q1: "Is this turn's output substantially better than the previous?" Q2: "Should we continue?"), each with 1-sentence rationale

- **Turn-Based Protocol** — Standardized execution protocol across all skills:
  - Turn 0: Initialization (create artifacts dir, parse input, set context, create logs)
  - Turn 1-N: STEP A (declare goal) -> STEP B (call base skill) -> STEP C (update artifacts) -> STEP D (2-question decision) -> STEP E (compliance self-audit) -> STEP F (stop signal check)
  - Forced exit when `turn_count >= max_turns` with `[ASSUMED]` annotation for incomplete items
  - Normal completion when ALL stop signals (V1-V5 AND Q1-Q4) satisfied simultaneously

- **Error Handling Matrix** — Each skill defines 5-7 error scenarios (E1-E7) with id, scenario, severity level (fatal/high/medium/low), and response protocol. Fatal errors (e.g., E1: "Phase contract violation") trigger immediate termination; lower severity errors trigger retry or degraded continuation.

- **Pipeline Orchestration** — `loop-pipeline` chains skills sequentially with data passing through shared artifacts in `.claude/loop-pipeline/`. Stage gates between phases validate required outputs exist before proceeding. Pipeline-level compliance logging tracks which skills ran and their exit status.

- **CI Validation** — `.github/workflows/validate-skills.yml` provides automated validation of all SKILL.md files. Checks YAML frontmatter (phase, max_turns, category fields), PHASE_CONTRACT block completeness (expected_outputs, banned_behaviors, stop_signal, decision_rules), LOOP EXECUTION PROTOCOL presence, and skill title format. Triggered on push/PR to main/master when SKILL.md files change, plus manual workflow_dispatch.

### Platform

- **Claude Code >= 2.1.0** required as runtime platform (leverages latest agentic capabilities and skill loading infrastructure)
- **Superpowers >= 1.0.0** required as base skill dependency (provides brainstorming, planning, executing, debugging, tdd, verification base skills)
- Zero compiled code — pure SKILL.md + protocol architecture
- No npm/pip dependencies, no build step, no binary artifacts
- Compatible with any Claude Code installation supporting the skill system (cross-platform: Linux, macOS, Windows via WSL)

### Documentation

- README.md (bilingual: Chinese + English) — Quick start, architecture overview, skill listing
- DESIGN.md — Full architecture design document (581 lines, 10 design decisions with rationale and trade-offs)
- IMPLEMENTATION_PLAN.md — 5-milestone structured implementation plan (694 lines) covering skill skeleton, phase contracts, protocol wiring, pipeline orchestration, and validation
- SKILL_VALIDATION.md — 10-item structural compliance verification checklist (all 7 skills PASS with details)
- SKILL_CI_VALIDATION.md — CI/CD validation design and test plan
- VERIFICATION_CHECKLIST.md — Manual verification procedures for each skill
- QUALIFICATION_STATEMENT.md — Argument for correctness of "zero code" architecture, addressing common concerns about skill-only implementations
- SUFFICIENCY_DECLARATION.md — Scope and completeness declaration (~95% sufficiency), listing remaining known gaps
- CONTRIBUTING.md — Contribution guide with issue templates (bug report, skill proposal, protocol change), PR process, and E2E test requirements
- pipeline-config.json / pipeline-config.strict.json / pipeline-config.test.json — Pipeline configuration presets for production, strict, and test environments
