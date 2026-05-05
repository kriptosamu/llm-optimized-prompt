# LLM Optimized Prompt

A compact, universal system prompt for AI assistants.
Reasoning-enhanced, token-efficient, designed for injection into any LLM or AI editor.

---

## The Prompt

### Balanced (recommended default)
```
You are an expert [domain].
Before answering, silently: identify problem type, consider edge cases, reason thoroughly.
Output: minimal — [format] only, no explanation unless asked.
No greetings, filler, hedging, or repetition.
Ambiguous? Ask 1 question. Else assume and state it explicitly.
```

### Maximum efficiency
```
Before answering, silently: identify problem type, consider edge cases.
Output: minimal. No explanation unless asked.
No greetings, filler, hedging, or repetition.
Ambiguous? Ask 1 question. Else assume and state it explicitly.
```

### Maximum quality (higher token cost)
```
Before answering: identify problem type, consider edge cases,
counterarguments, and second-order effects.
Show your work. Flag all assumptions.
Output: structured — use headers and bullets.
```

---

## What It Does

| Behavior | Result |
|----------|--------|
| Terse output | No filler, direct answers |
| Silent reasoning | Internal reasoning on standard models, minimal visible output |
| Smart clarification | Asks when blocked, assumes and **states it** when clear |
| Format enforcement | Code, bullets, or text — nothing extra |
| Hallucination reduction | Assumptions made explicit, facts separated from inference |
| Domain priming | `You are an expert [domain]` activates relevant knowledge patterns |

---

## Why This Works

- **`silently` controls output verbosity** — keeps reasoning internal without bloating output on standard (non-reasoning) models
- **Separation of concerns** — reasoning quality and output verbosity are controlled independently
- **Explicit assumptions** — `state it explicitly` makes silent assumptions visible, reducing hallucination risk
- **Domain-aware** — sector-specific variants outperform generic prompts on specialized tasks
- **Scales** — same structure works from 1-shot chats to long agentic sessions

> **On XML tags:** These prompts use plain text, which parses across all major models. For Claude specifically, Anthropic recommends XML tags for complex, structured prompts — consider wrapping sections in XML if targeting Claude exclusively.

---

## Supported Platforms

**LLMs:** Claude, GPT-4, Gemini, Deepseek, Qwen, GLM, Kimi
**Editors & CLI:** Cursor, Windsurf, Claude Code, GitHub Copilot, Codex CLI, Opencode, Antigravity

---

## Quick Start

1. Pick a variant above (or a sector prompt from `prompt.md`)
2. Replace `[domain]` and `[format]` with your context
3. Paste into system instructions or editor rules file (see `guide.md`)
4. Verify with: *"What rules are you following?"*

> **Reasoning models** (Claude thinking, o1/o3, Gemini thinking): Remove `silently` — these models reason internally by default and the instruction is redundant.

---

## File Structure

```
.
├── readme.md            # This file — overview and quick start
├── prompt.md            # Sector-specific prompts (coding, data, writing, etc.)
├── prompt-tags.md       # Tag reference — cost, effect, combinations
└── guide.md             # Platform-specific injection instructions
```

---

## Tradeoffs

| Approach | Token cost | Reasoning | Hallucination risk |
|----------|-----------|-----------|-------------------|
| Maximum efficiency | ↓↓ | ↑ | ↑ (silent assumptions) |
| Balanced | ↓ | ↑↑ | ↓ (explicit assumptions) |
| Maximum quality | ↑↑ | ↑↑↑ | ↓↓ |
| Few-shot examples | ↑↑↑ (input) | ↑↑↑ | ↓↓↓ |

> No prompt eliminates hallucination — it only reduces it.