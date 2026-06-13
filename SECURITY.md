# Security Policy / 安全策略

> loop-superpowers | Version: 0.1.1 | Last Updated: 2026-06-13

---

## 1. Supported Versions / 支持的版本

| Version | Supported          | Notes |
|---------|-------------------|-------|
| 0.1.x   | ✅ Full support    | Current release |
| < 0.1.0 | ❌ Not supported   | Pre-release only |

## 2. Reporting a Vulnerability / 报告安全漏洞

**请勿公开披露安全漏洞。** 请通过以下渠道私密报告：

- **Email**: novelnexusai@outlook.com
- **GitHub**: [Private Security Advisory](https://github.com/PerryLink/loop-superpowers/security/advisories/new)

我们将在 48 小时内确认收到报告，并在 5 个工作日内提供初步评估。

### 报告应包含

1. 漏洞描述（发生了什么，在哪发生）
2. 复现步骤（最小可行复现）
3. 影响评估（潜在后果）
4. 建议修复方案（如有）

## 3. Security Model / 安全模型

### 3.1 项目性质

loop-superpowers 是**纯 Skill 定义项目**，不含编译代码、运行时环境或外部依赖。安全模型围绕以下核心：

| 层次 | 机制 | 说明 |
|------|------|------|
| **Skill 层** | Phase Contract | 每个 Skill 的 `<<<PHASE_CONTRACT>>>` 定义行为边界 |
| **协议层** | 禁止行为清单 | 每个 Skill 5-7 项禁止行为，含严重性等级 |
| **Pipeline 层** | 阶段门禁 | `loop-pipeline` 阶段间验证检查 |
| **CI 层** | 自动验证 | `.github/workflows/validate-skills.yml` 格式校验 |

### 3.2 威胁模型

由于项目不含可执行代码，传统攻击面（代码注入、依赖漏洞、内存安全）**不适用**。

**唯一风险面：Skill 指令注入（Prompt Injection）**

- **攻击场景**：恶意用户构造输入，绕开 Phase Contract 行为边界
- **防护措施**：
  1. Phase Contract 的 `banned_behaviors` 定义明确的行为禁止清单
  2. `<<<TURN_START>>>` 和 `<<<SELF_AUDIT_START>>>` 机制每轮自检
  3. `stop_signals` 复合条件确保异常行为触发终止
  4. `max_turns` 提供绝对终止上限
- **残余风险**：Phase Contract 依赖 LLM 的指令遵循能力，无法提供硬性沙盒保证。这与所有基于 LLM 的系统一致。

### 3.3 文件系统安全

- Skill 操作范围受 `allowed_file_scope` 限制
- 每个 Skill 仅能修改其专属 `artifacts/` 目录
- `loop-pipeline` 的数据传递仅通过受控的共享 artifacts 路径

## 4. Dependency Security / 依赖安全

loop-superpowers **无运行时依赖**：

| 依赖类型 | 状态 |
|---------|------|
| npm 包 | 无 |
| pip 包 | 无 |
| 系统库 | 无 |
| 外部 API | 无 |
| 平台依赖 | Claude Code >= 2.1.0 + Superpowers >= 1.0.0 |

平台级安全由 Claude Code 和 Superpowers 上游项目负责。

## 5. Configuration Security / 配置安全

### pipeline-config.json 安全

- `pipeline-config.json`：生产环境，宽松配置
- `pipeline-config.strict.json`：严格模式，全部门禁开启
- `pipeline-config.test.json`：测试环境，允许调试

**建议**：生产环境使用 `pipeline-config.strict.json`。

### 敏感信息

loop-superpowers **不会**处理或存储：
- API 密钥或认证凭据
- 个人信息 (PII)
- 机密业务数据
- 任何形式的加密材料

## 6. Security Contact / 安全联系

- **Email**: novelnexusai@outlook.com
- **GitHub**: [@PerryLink](https://github.com/PerryLink)
- **Response Time**: < 48 hours acknowledgment, < 5 business days assessment

## 7. Disclosure Policy / 披露政策

1. 报告提交 → 2. 确认（48h内） → 3. 调查修复（5-15工作日） → 4. 发布修复 → 5. 公开披露（修复后30天或协商确定）

我们遵循 [Responsible Disclosure](https://en.wikipedia.org/wiki/Responsible_disclosure) 原则。

---

*Security is a shared responsibility. Thank you for helping keep loop-superpowers safe.*
*安全是共同责任。感谢你帮助保持 loop-superpowers 的安全。*
