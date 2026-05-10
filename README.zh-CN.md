# Documentation Skill

Documentation Skill 是一份面向编码 Agent 的文档维护 Skill，用来在代码、API、配置、架构、部署、运维或重要决策发生变化后，让项目文档保持准确，同时避免无意义的文档噪音。

它适合已经在仓库内工作的 Agent：Agent 可以判断当前任务是否真的影响文档、应该更新哪一层文档，以及什么时候应该明确说明“不需要改文档”。

## 快速开始

安装插件，或把 skill 复制到你的 Agent skills 目录，然后在项目级 Agent 指南中加入：

```md
Use the documentation skill before completing tasks that may change public behavior, APIs, CLI commands, configuration, setup, architecture, deployment, operations, or durable project decisions.
```

这个 skill 不会默认重写整套文档。它会检查当前任务是否影响文档，只更新相关文件，并在无需更新时明确说明原因。

## 工作方式

任务完成前，skill 会让 Agent 检查三个问题：

1. 接口是否变化：公开行为、API、路由、CLI 命令、配置、环境变量、schema、文件格式、安装或使用方式。
2. 结构是否变化：架构、模块职责、依赖边界、部署、运维或贡献者工作流。
3. 项目知识是否变化：长期决策、重要取舍、已知限制或未来维护者需要知道的技术债。

如果答案是“是”，Agent 会更新最小且相关的文档范围。如果答案是“否”，Agent 会保持文档不变，并在最终回复中说明已检查且无需更新。

## 安装

不同 Agent 宿主的安装方式不同。如果你同时使用多个宿主，需要分别安装。

### Codex

本仓库包含 Codex 插件元数据：

```txt
.codex-plugin/plugin.json
```

仓库发布后，可以通过 Codex 插件流程安装；也可以直接复制 skill：

```txt
$CODEX_HOME/skills/documentation/
```

如果没有设置 `CODEX_HOME`，请使用你系统上的 Codex 默认 skills 目录。

### Claude Code

本仓库包含 Claude 插件元数据：

```txt
.claude-plugin/plugin.json
```

如果你的 Claude Code 环境支持从仓库安装插件，可以直接安装；也可以把 `skills/documentation/` 复制到 Claude skills 目录。

### Cursor

本仓库包含 Cursor 插件元数据：

```txt
.cursor-plugin/plugin.json
```

该 manifest 指向：

```txt
./skills/
```

### Gemini CLI

本仓库包含：

```txt
gemini-extension.json
GEMINI.md
```

`GEMINI.md` 会直接加载 documentation skill：

```md
@./skills/documentation/SKILL.md
```

### OpenCode

本仓库包含 OpenCode 插件入口：

```txt
package.json
.opencode/plugins/documentation-skill.js
.opencode/INSTALL.md
```

仓库发布后，在 `opencode.json` 中加入：

```json
{
  "plugin": ["documentation-skill@git+https://github.com/<owner>/documentation-skill.git"]
}
```

本地测试时，可以让 OpenCode 指向当前仓库路径。更多说明见 `.opencode/INSTALL.md`。

### 项目内本地 Skill

任何支持本地 skills 的宿主，都可以直接把 skill 目录复制到项目中：

```txt
your-project/
└── skills/
    └── documentation/
        ├── SKILL.md
        ├── agents/
        └── references/
```

## 会更新什么

这个 skill 的策略是保守的：优先做小范围精准编辑，避免因为内部实现调整或机械清理而制造文档 churn。

典型更新范围包括：

- README 中的快速开始、安装、使用方式或文档索引
- public API、CLI 命令、配置、环境变量、schema、文件格式和错误说明的 reference docs
- 模块边界、依赖关系或数据流变化时的 architecture docs
- 面向用户的发布、破坏性变更和废弃项对应的 changelog 或 release notes
- 只有在决策长期有效且有重要取舍时才记录 ADR
- 可重复执行的运维或维护流程对应的 playbook
- 已存在或明确要求的项目级 Agent 指南

## 仓库内容

```txt
.claude-plugin/
└── plugin.json
.codex-plugin/
└── plugin.json
.cursor-plugin/
└── plugin.json
.opencode/
├── INSTALL.md
└── plugins/
    └── documentation-skill.js
AGENTS.md
CLAUDE.md
gemini-extension.json
GEMINI.md
package.json
skills/documentation/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── adr.md
    ├── bootstrap.md
    ├── document-map.md
    └── templates.md
```

`SKILL.md` 包含核心工作流和安全边界。`references/` 中的文件只在 Agent 需要更详细模板或说明时加载，从而保持主 skill 轻量。

## 设计原则

- 证据优先：文档必须来自代码、配置、测试、示例、发布元数据、现有文档或用户明确说明。
- 最小有效编辑：只更新能让项目保持准确的最小文档范围。
- 不创建空文档：不创建占位文件、空章节、空表格或猜测性的路线图。
- 尊重现有结构：如果项目已有清晰的文档结构和风格，优先沿用。
- 生产安全：不要记录 secrets、私有凭据、内部 token 或敏感客户数据。

## 校验

发布前校验 skill metadata：

```sh
python path/to/skill-creator/scripts/quick_validate.py skills/documentation
```

也可以检查 JSON manifest：

```sh
python -m json.tool .codex-plugin/plugin.json
python -m json.tool .claude-plugin/plugin.json
python -m json.tool .cursor-plugin/plugin.json
python -m json.tool gemini-extension.json
python -m json.tool package.json
```

## 发布清单

发布到 GitHub 前建议检查：

- 将 `.opencode/INSTALL.md` 中的 `<owner>` 替换成最终 GitHub 账号或组织名。
- 如果分发流程需要，在 `.codex-plugin/plugin.json` 中补充 `homepage`、`repository` 和 `interface.websiteURL`。
- 至少在一个目标宿主中安装并确认能发现 `documentation` skill。
- 运行上面的校验命令。

## 许可证

MIT License。详见 [LICENSE](LICENSE)。
