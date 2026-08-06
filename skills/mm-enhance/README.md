# MM-enhance

`MM-enhance` 是一个 Prompt 增强 skill。它把粗糙、口语化、上下文不完整的指令，改写成更清楚、可独立执行的 Prompt。

运行时 skill id 是 `mm-enhance`。

## 安装

把本目录复制到你的 agent skills 目录：

```text
skills/mm-enhance/
```

Codex：

```bash
mkdir -p ~/.codex/skills/mm-enhance
cp -R skills/mm-enhance/. ~/.codex/skills/mm-enhance/
```

Claude Code：

```bash
mkdir -p ~/.claude/skills/mm-enhance
cp -R skills/mm-enhance/. ~/.claude/skills/mm-enhance/
```

## 调用

Codex：

```text
$mm-enhance <你的原始提示词>
```

Claude Code：

```text
/mm-enhance <你的原始提示词>
```

## 内容

- `SKILL.md`：skill 入口和触发说明
- `references/workflow.md`：核心工作流
- `agents/openai.yaml`：OpenAI agent 元数据
