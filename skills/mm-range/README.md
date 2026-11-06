# MM-range

跨领域组队。把一份重要交付物从「名词」改写成「动词」，拆出它真正要完成的几个动作，为每个动作找最擅长的领域（含红队），让每个角色实际去做研究、计算、改稿，最后合成并用外部裁判验收。

运行时 skill id 是 `mm-range`。

## 安装

把本目录复制到你的 agent skills 目录。

Codex：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.codex/skills/mm-range
cp -R "$tmpdir/MnMei-skill/skills/mm-range/." ~/.codex/skills/mm-range/
```

Claude Code：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.claude/skills/mm-range
cp -R "$tmpdir/MnMei-skill/skills/mm-range/." ~/.claude/skills/mm-range/
```

## 调用

- Codex：`$mm-range <你的任务或 prompt>`
- Claude Code：`/mm-range <你的任务或 prompt>`

## 内容

- `SKILL.md`：skill 入口、触发说明和完整工作流
- `agents/openai.yaml`：OpenAI agent 元数据
