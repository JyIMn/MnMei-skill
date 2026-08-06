# 安装说明

`MM-enhance` 是一个轻量 Agent Skill。它不需要 Python、Node.js 或额外 API key。

Agent Skills 的机器可读名称需要使用小写 kebab-case，所以实际安装和调用名是 `mm-enhance`；`MM-enhance` 是对外展示名。

这个仓库是多 skill 集合。不要把整个仓库直接 clone 成一个 skill；要安装的是子目录：

```text
skills/mm-enhance/
```

## Codex

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.codex/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.codex/skills/mm-enhance/
```

然后重启 Codex，或开启一个新任务。调用方式：

```text
$mm-enhance <你的原始提示词>
```

## Claude Code

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.claude/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.claude/skills/mm-enhance/
```

然后重启 Claude Code，或开启一个新会话。调用方式：

```text
/mm-enhance <你的原始提示词>
```

## 其他支持 Agent Skills 的工具

把 `skills/mm-enhance/` 这个子目录复制到该工具的 skills 目录，并确保目录名是：

```text
mm-enhance
```

目录里至少要包含：

```text
SKILL.md
references/workflow.md
```

## 更新

重新覆盖安装当前子目录内容：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.codex/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.codex/skills/mm-enhance/
```

Claude Code 用户把目标路径换成：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.claude/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.claude/skills/mm-enhance/
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
