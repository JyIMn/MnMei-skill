---
name: mm-enhance
description: Use when the user provides a rough instruction, asks to optimize or rewrite a prompt, wants a prompt prepared for another AI chat, wants help surfacing the real problem behind a prompt, or replies with a short confirmation such as "继续执行", "用这个开始", "直接开始", or "run with this prompt" after a prompt-enhancement step in the same conversation.
---

# MM-enhance

`MM-enhance` is the public display name. The runtime skill id is `mm-enhance`.

This skill turns a rough instruction into a clearer, less ambiguous prompt that can stand on its own.

Use this skill for prompt improvement, prompt rewriting, and prompt-to-execution handoff.

Invocation examples:

- Codex: `$mm-enhance <prompt>`
- Claude Code: `/mm-enhance <prompt>`

Read [references/workflow.md](references/workflow.md) before responding and follow it as the authoritative workflow.
