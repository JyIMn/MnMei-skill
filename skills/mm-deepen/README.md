# MM-deepen

做深不做大。拿到任务或 prompt 后先回答四问——顶尖专家会多做什么、从哪份最原始的素材入手、用什么具体方法和工具、除了你和 AI 还有什么能证明结果对——再把任务重写成专家级版本。

运行时 skill id 是 `mm-deepen`。

## 安装

把本目录复制到你的 agent skills 目录。

Codex：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.codex/skills/mm-deepen
cp -R "$tmpdir/MnMei-skill/skills/mm-deepen/." ~/.codex/skills/mm-deepen/
```

Claude Code：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.claude/skills/mm-deepen
cp -R "$tmpdir/MnMei-skill/skills/mm-deepen/." ~/.claude/skills/mm-deepen/
```

## 调用

- Codex：`$mm-deepen <你的任务或 prompt>`
- Claude Code：`/mm-deepen <你的任务或 prompt>`

## 内容

- `SKILL.md`：skill 入口、触发说明和完整工作流
- `agents/openai.yaml`：OpenAI agent 元数据
