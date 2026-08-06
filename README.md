# MnMei Skill

面向 MnMei AI 社群公开分享的 Agent Skills 仓库。

当前公开的第一个 skill 是 `MM-enhance`：把一段粗糙指令改写成更清晰、可独立执行的 Prompt，并在必要时帮你看见指令背后的真实问题或决策点。

说明：Agent Skills 的机器可读名称需要使用小写 kebab-case，所以实际安装和调用名是 `mm-enhance`；`MM-enhance` 是对外展示名。

## 仓库结构

这个仓库是一个多 skill 集合，不是单 skill 仓库。每个 skill 都放在 `skills/<skill-id>/` 下面，后续新增 skill 也按这个结构扩展。

```text
skills/
  mm-enhance/
    SKILL.md
    references/
    agents/
```

## 当前 Skill

| Skill | 用途 | 入口文件 |
|---|---|---|
| `MM-enhance` / `mm-enhance` | 优化 Prompt、补齐上下文、澄清目标、保留原意 | [`skills/mm-enhance/SKILL.md`](skills/mm-enhance/SKILL.md) |

## 适合什么场景

- 你要把一句模糊想法交给 AI 执行，但担心它理解偏。
- 你想把口语化需求改成可以复制到另一个 AI 对话里的 Prompt。
- 你知道自己想要一个结果，但还没说清楚输出格式、约束、判断标准。
- 你怀疑表层问题背后还有一个更重要的决策，需要 AI 顺手帮你点出来。

## 不适合什么场景

- 不适合替代事实核查、网页搜索或代码执行。
- 不适合在你只想要直接答案时强行扩写。
- 不适合把私人资料、账号、token、客户信息直接塞进公开 Prompt。

## 快速安装

### 方式一：让你的 AI Agent 安装

在支持 Agent Skills 的工具里，对你的 agent 说：

```text
帮我安装这个 skill：https://github.com/JyIMn/MnMei-skill/tree/main/skills/mm-enhance
安装后 skill 名称使用 mm-enhance，展示名是 MM-enhance。
```

### 方式二：手动安装到 Codex

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.codex/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.codex/skills/mm-enhance/
```

重启 Codex 或开启新任务后，使用：

```text
$mm-enhance <你的原始提示词>
```

### 方式三：手动安装到 Claude Code

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.claude/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.claude/skills/mm-enhance/
```

然后在 Claude Code 中使用：

```text
/mm-enhance <你的原始提示词>
```

更多细节见 [`INSTALL.md`](INSTALL.md)。

## 使用示例

```text
$mm-enhance 我想让 AI 帮我研究一个同行账号为什么火，然后给我一套我自己能用的内容选题方向
```

它会先输出：

- 原始意图
- 必要时补出的深层需求
- 做了哪些改写
- 可复制的增强版 Prompt
- 是否继续执行的确认问题

## 更新

如果已经安装过，可以重新覆盖安装当前子目录内容。

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.codex/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.codex/skills/mm-enhance/
```

Claude Code 用户把路径换成：

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 https://github.com/JyIMn/MnMei-skill.git "$tmpdir/MnMei-skill"
mkdir -p ~/.claude/skills/mm-enhance
cp -R "$tmpdir/MnMei-skill/skills/mm-enhance/." ~/.claude/skills/mm-enhance/
```

## 许可

此仓库当前未附加开源许可证。公开访问不等于自动授予商业再分发、改名转售或二次发布权利；社群成员可以按本 README 安装和学习使用。
