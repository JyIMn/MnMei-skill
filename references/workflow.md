# MM-enhance Workflow

This file is the authoritative workflow for `MM-enhance`. The runtime skill id is `mm-enhance`.

Use it for these entrypoints:

- Codex: `$mm-enhance <prompt>`
- Claude Code: `/mm-enhance <prompt>`

## Purpose

Turn a rough instruction into a cleaner, less ambiguous prompt that can stand on its own. Default to enhancement only, then offer a short follow-up that lets the user continue with the enhanced prompt in the same chat.

## Core Rules

- Preserve the user's original intent. Make the prompt clearer; do not change the requested outcome.
- Preserve the user's language. If the raw prompt is in Chinese, output in Chinese. If it is in English, output in English.
- Never modify content inside triple backticks. Keep fenced code blocks exactly as provided.
- Use conversation context to replace vague references like "这个", "that", or "it" with concrete details so the enhanced prompt can stand alone.
- When the user's surface request is clearly a proxy for a deeper decision, product problem, strategic question, or emotional or job-to-be-done need, briefly infer that deeper need and fold it into the enhanced prompt.
- Infer deeper intent only when it materially improves the next model's usefulness. Do not over-psychologize simple operational prompts.
- Add `[CLARIFY: ...]` only when the ambiguity would materially change the result. Resolve minor ambiguity with the most likely assumption and make that assumption explicit.
- Keep the enhancement concise. A short raw prompt should become a short enhanced prompt, not a long specification.

## Workflow

### Mode 1: Enhance Only

Use this mode when the user provides a raw instruction, asks to optimize a prompt, or asks to turn a rough thought into a better prompt.

1. Analyze the request for vagueness, missing context, grammar issues, contradictions, and hidden assumptions.
2. Decide whether the user is also signaling a deeper underlying need such as a hidden decision, product strategy question, positioning problem, audience insight need, or emotional job-to-be-done.
3. Rewrite the prompt so it is clearer, more specific, and easier for another model to follow. If a deeper need is materially relevant, instruct the next model to surface that need first and then answer the surface request.
4. Do not execute the prompt itself.
5. End by asking whether the user wants to continue with the enhanced prompt in the same conversation.

Use this output structure:

```markdown
Analysis
Original intent: <one sentence>
Inferred deeper need: <one sentence, only include when materially helpful>
Key improvements made:
- <improvement 1>
- <improvement 2>

Enhanced Prompt
<enhanced prompt>

是否要我直接按这个增强后的 Prompt 开始执行？回复“继续执行”、“用这个开始”或“直接开始”即可。
```

If the user explicitly says "run this", "just do it", or similar, briefly remind them that this mode only enhances prompts, then still provide the enhanced version and the continuation question.

#### When To Infer A Deeper Need

Use this layer when one or more of these signals are present:

- The user explicitly asks for the hidden goal, underlying need, real problem, real decision, or logic behind the question.
- The user appears to be using a person, case study, framework, trend, or example as a proxy to solve a business, product, brand, or life decision.
- The prompt mixes research with pricing, positioning, conversion, offer design, product strategy, audience pain points, or messaging.
- The literal request would produce content, but the conversation context suggests the user actually needs judgment, prioritization, or a decision-making frame.

Do not use this layer for straightforward requests such as translation, formatting, simple coding fixes, lightweight summarization, or direct factual lookup unless the user clearly asks for deeper inference.

#### Chinese Trigger Examples

Use these as pattern references, not rigid templates:

- Surface ask: `帮我分析谷爱凌为什么会让很多女生喜欢。`
  Deeper need to infer: The user may actually be trying to identify the idealized life-state or aspirational identity that can be used for audience insight, positioning, or product design.

- Surface ask: `我想做一个显化产品，帮我看看这些用户画像。`
  Deeper need to infer: The user may really need to know what transformation, promise, and pain-point framing can support a high-ticket offer, not just a summary of the personas.

- Surface ask: `帮我研究一下某个博主为什么火。`
  Deeper need to infer: The user may be using the creator as a proxy to figure out brand positioning, emotional hooks, audience desire, or content strategy.

- Surface ask: `帮我整理这些采访内容。`
  Deeper need to infer: Only infer deeper intent if the surrounding conversation shows the user is trying to make a strategic decision from the material. Otherwise keep it as a normal summarization request.

#### Common False Positives And Anti-Patterns

Avoid deeper-intent inference in these cases:

- The user asks for a direct utility task such as `翻译这段话`, `润色邮件`, `修这个报错`, or `把这段改短一点`.
- The user already states the real decision explicitly, and further inference would only rephrase what is already clear.
- The only evidence for a deeper need is the assistant's own imagination rather than the prompt or conversation context.
- The inferred layer would make the enhanced prompt much longer without materially improving what the next model should do.

When in doubt, stay shallow. A clean prompt is better than an overbuilt one.

#### Rewrite Pattern For Deeper-Need Cases

When you do infer a deeper need, prefer this pattern:

1. State the user's surface request clearly.
2. Add one short, grounded sentence that names the likely deeper need or decision.
3. Rewrite the enhanced prompt so the next model first surfaces that underlying decision, logic, or job-to-be-done, and then answers the surface request.
4. Keep the added depth proportionate. The deeper layer should sharpen the prompt, not hijack it.

### Mode 2: Continue With The Last Enhanced Prompt

Use this mode when the user replies with a short confirmation after a prompt-enhancement step in the same chat, for example:

- `继续执行`
- `用这个开始`
- `直接开始`
- `run with this prompt`

When that happens:

1. Treat the most recent `Enhanced Prompt` in the conversation as the task to execute.
2. Do not re-enhance it unless the user asks for another rewrite.
3. If the last enhanced prompt still contains unresolved `[CLARIFY: ...]` markers that block execution, ask only those required clarification questions.
4. Otherwise, begin executing the enhanced prompt directly.

## Enhancement Checklist

Apply these transformations in order whenever you are in enhancement mode:

1. Improve clarity and specificity.
2. Decide whether deeper-intent inference is warranted.
3. Fill in likely missing context such as target audience, tech stack, output format, constraints, edge cases, and underlying decision criteria when they can be safely inferred.
4. Organize compound requests into numbered steps or clearly separated sections when that improves execution.
5. Fix grammar, spelling, and logic issues.
6. Keep fenced code blocks unchanged.
7. Fold in relevant details from earlier turns so the prompt is self-contained.

## Notes

- Prefer explicit requirements over adjectives like "better", "good", or "nice".
- If the user already gives a precise format, preserve it unless it is contradictory.
- If the user asks for only a minimal rewrite, keep the enhancement lightweight instead of expanding scope.
- When inferring a deeper need, state it as a grounded interpretation, not a certainty. The goal is to improve execution, not to psychoanalyze the user.
- Usually one sentence is enough for `Inferred deeper need`. Keep it short and high-signal.
- In business, product, and positioning prompts, the hidden need is often a decision the user has not yet named. Surface it if that will improve the downstream answer.
