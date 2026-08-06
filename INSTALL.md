# 安装说明

`MM-enhance` 是一个轻量 Agent Skill。它不需要 Python、Node.js 或额外 API key；安装本质上就是把这个仓库放到你的 agent 的 skills 目录里。

Agent Skills 的机器可读名称需要使用小写 kebab-case，所以实际安装和调用名是 `mm-enhance`；`MM-enhance` 是对外展示名。

## Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/JyIMn/MnMei-skill.git ~/.codex/skills/mm-enhance
```

然后重启 Codex，或开启一个新任务。调用方式：

```text
$mm-enhance <你的原始提示词>
```

## Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/JyIMn/MnMei-skill.git ~/.claude/skills/mm-enhance
```

然后重启 Claude Code，或开启一个新会话。调用方式：

```text
/mm-enhance <你的原始提示词>
```

## 其他支持 Agent Skills 的工具

把本仓库 clone 到该工具的 skills 目录，并确保目录名是：

```text
mm-enhance
```

目录里至少要包含：

```text
SKILL.md
references/workflow.md
```

## 更新

Codex：

```bash
cd ~/.codex/skills/mm-enhance
git pull
```

Claude Code：

```bash
cd ~/.claude/skills/mm-enhance
git pull
```

## 卸载

Codex：

```bash
rm -rf ~/.codex/skills/mm-enhance
```

Claude Code：

```bash
rm -rf ~/.claude/skills/mm-enhance
```

## 验证

安装后新开一个对话，输入：

```text
$mm-enhance 帮我把这个想法整理成一个能交给 AI 执行的提示词
```

如果正常工作，它会输出 `Analysis`、`Enhanced Prompt`，并询问是否继续执行。
